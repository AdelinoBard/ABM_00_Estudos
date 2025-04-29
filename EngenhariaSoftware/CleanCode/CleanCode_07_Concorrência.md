# **Concorrência em C# e Código Limpo**

Os princípios de Código Limpo se aplicam igualmente bem ao desenvolvimento de código concorrente em C#. Clareza, simplicidade e tratamento adequado de erros são cruciais para evitar problemas difíceis de depurar em cenários com múltiplas threads.

## Use `Task` e `async`/`await`, não Callbacks Aninhados

Callbacks em C# (como o uso excessivo de `ContinueWith` sem um bom tratamento de exceções) podem levar a um código complexo e difícil de manter. A abordagem moderna e mais limpa em C# é utilizar `async` e `await` em conjunto com `Task` para operações assíncronas.

**Ruim (Exemplo conceitual, callbacks explícitos não são tão comuns em cenários modernos de IO em C#):**

```csharp
// Exemplo conceitual simulando callbacks
public class CallbackHell
{
    public void DownloadFile(string url, Action<string, Exception> completed)
    {
        var webClient = new WebClient();
        webClient.DownloadStringCompleted += (sender, e) =>
        {
            if (e.Error != null)
            {
                completed(null, e.Error);
                return;
            }

            WriteFile("article.html", e.Result, (success, writeError) =>
            {
                if (writeError != null)
                {
                    completed(null, writeError);
                    return;
                }

                completed("File written", null);
            });
        };
        webClient.DownloadStringAsync(new Uri(url));
    }

    public void WriteFile(string path, string content, Action<bool, Exception> completed)
    {
        try
        {
            File.WriteAllText(path, content);
            completed(true, null);
        }
        catch (Exception ex)
        {
            completed(false, ex);
        }
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        var callbackHell = new CallbackHell();
        callbackHell.DownloadFile("https://en.wikipedia.org/wiki/Robert_Cecil_Martin", (result, error) =>
        {
            if (error != null)
            {
                Console.WriteLine($"Error: {error.Message}");
            }
            else
            {
                Console.WriteLine(result);
            }
        });

        Console.ReadKey();
    }
}
```

**Bom:**

```csharp
using System.Net.Http;
using System.IO;
using System.Threading.Tasks;
using System;

public class CleanConcurrency
{
    public async Task GetCleanCodeArticleAsync()
    {
        try
        {
            using (var httpClient = new HttpClient())
            {
                var response = await httpClient.GetStringAsync("https://en.wikipedia.org/wiki/Robert_Cecil_Martin");
                await File.WriteAllTextAsync("article.html", response);
                Console.WriteLine("File written");
            }
        }
        catch (HttpRequestException ex)
        {
            Console.WriteLine($"Error downloading file: {ex.Message}");
        }
        catch (IOException ex)
        {
            Console.WriteLine($"Error writing file: {ex.Message}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"An unexpected error occurred: {ex.Message}");
        }
    }
}

public class Program
{
    public static async Task Main(string[] args)
    {
        var cleanConcurrency = new CleanConcurrency();
        await cleanConcurrency.GetCleanCodeArticleAsync();

        Console.ReadKey();
    }
}
```

## `async`/`await` Tornam o Código Assíncrono Imperativo e Limpo

Assim como em JavaScript, `async` e `await` em C# simplificam significativamente o código assíncrono. Ao marcar um método com `async`, você pode usar a palavra-chave `await` para pausar a execução do método até que uma operação assíncrona (que retorna um `Task` ou `Task<T>`) seja concluída. Isso permite escrever código assíncrono que se parece muito com código síncrono, facilitando a leitura e a manutenção.

**Ruim (Usando `Task.ContinueWith` de forma aninhada):**

```csharp
using System.Net.Http;
using System.IO;
using System.Threading.Tasks;
using System;

public class NotSoCleanConcurrency
{
    public Task GetCleanCodeArticleAsync()
    {
        var httpClient = new HttpClient();
        return httpClient.GetStringAsync("https://en.wikipedia.org/wiki/Robert_Cecil_Martin")
            .ContinueWith(taskResponse =>
            {
                if (taskResponse.IsFaulted)
                {
                    Console.WriteLine($"Error downloading file: {taskResponse.Exception?.InnerException?.Message}");
                    return Task.CompletedTask;
                }

                return File.WriteAllTextAsync("article.html", taskResponse.Result)
                    .ContinueWith(taskWrite =>
                    {
                        if (taskWrite.IsFaulted)
                        {
                            Console.WriteLine($"Error writing file: {taskWrite.Exception?.InnerException?.Message}");
                        }
                        else
                        {
                            Console.WriteLine("File written");
                        }
                    });
            }).Unwrap();
    }
}

public class Program
{
    public static async Task Main(string[] args)
    {
        var notSoCleanConcurrency = new NotSoCleanConcurrency();
        await notSoCleanConcurrency.GetCleanCodeArticleAsync();

        Console.ReadKey();
    }
}
```

**Bom (Usando `async`/`await`):**

```csharp
using System.Net.Http;
using System.IO;
using System.Threading.Tasks;
using System;

public class CleanConcurrencyAsyncAwait
{
    public async Task GetCleanCodeArticleAsync()
    {
        try
        {
            using (var httpClient = new HttpClient())
            {
                var response = await httpClient.GetStringAsync("https://en.wikipedia.org/wiki/Robert_Cecil_Martin");
                await File.WriteAllTextAsync("article.html", response);
                Console.WriteLine("File written");
            }
        }
        catch (HttpRequestException ex)
        {
            Console.WriteLine($"Error downloading file: {ex.Message}");
        }
        catch (IOException ex)
        {
            Console.WriteLine($"Error writing file: {ex.Message}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"An unexpected error occurred: {ex.Message}");
        }
    }
}

public class Program
{
    public static async Task Main(string[] args)
    {
        var cleanConcurrencyAsyncAwait = new CleanConcurrencyAsyncAwait();
        await cleanConcurrencyAsyncAwait.GetCleanCodeArticleAsync();

        Console.ReadKey();
    }
}
```

**Outras Práticas de Código Limpo Relevantes para Concorrência em C#:**

* **Responsabilidade Única:** Classes e métodos relacionados à concorrência devem ter uma única responsabilidade bem definida (por exemplo, gerenciar uma fila de trabalho, executar uma tarefa específica de forma assíncrona).

* **Nomes Significativos:** Variáveis, parâmetros e métodos relacionados a operações assíncronas devem ter nomes claros que indiquem sua natureza (por exemplo, `DownloadFileAsync`, `cancellationToken`).

* **Tratamento de Erros Robusto:** Use blocos `try-catch` para lidar com exceções que podem ocorrer em operações assíncronas. Considere o uso de `CancellationToken` para permitir o cancelamento de tarefas longas.

* **Sincronização Cuidadosa:** Ao compartilhar recursos entre threads, use mecanismos de sincronização como `lock`, `Mutex`, `SemaphoreSlim` com cautela para evitar deadlocks e condições de corrida. Mantenha as seções sincronizadas o mais curtas possível.

* **Abstrações de Concorrência:** Considere o uso de abstrações de nível superior como `Task.Run`, `Parallel.ForEach`, `BlockingCollection` e `Async/Await` para simplificar o código concorrente e evitar a manipulação manual de threads sempre que possível.

* **Testes Concorrentes:** Escrever testes que exercitem o código em cenários concorrentes é fundamental para garantir sua correção e robustez.

---