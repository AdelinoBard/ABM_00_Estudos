














## 11. Inicializadores de Objetos  

Os **inicializadores de objeto** permitem criar um objeto e definir suas propriedades `public` (e variáveis de instância `public`, se houver) na mesma instrução. Isso é útil quando uma classe não possui um construtor que atenda às suas necessidades, mas oferece um construtor sem argumentos e propriedades acessíveis para configuração dos dados.  

O exemplo a seguir demonstra o uso de inicializadores de objeto com a classe `Time2`:  

```csharp
// cria um objeto Time2 e inicializa suas propriedades
var aTime = new Time2 {Hour = 14, Minute = 30, Second = 12};

// cria um objeto Time2 e inicializa apenas a propriedade Minute
var anotherTime = new Time2 {Minute = 45};
```  

Na primeira declaração, um objeto `Time2` chamado `aTime` é criado utilizando o construtor sem argumentos da classe `Time2`. Em seguida, um **inicializador de objeto** é aplicado para definir as propriedades `Hour`, `Minute` e `Second`. Note que `new Time2` é seguido imediatamente por uma **lista de inicializadores de objeto** — um conjunto de atribuições entre chaves (`{ }`), onde cada propriedade recebe um valor específico. Cada propriedade pode aparecer apenas _uma vez_ na lista de inicialização, e as atribuições são processadas na ordem em que aparecem.  

Na segunda declaração, um novo objeto `Time2` chamado `anotherTime` é criado da mesma maneira, mas apenas a propriedade `Minute` é definida. Como o construtor `Time2` sem argumentos inicializa o objeto para a meia-noite, as propriedades `Hour` e `Second` permanecem com seus valores padrão (zero), pois não foram explicitamente definidas no inicializador de objeto.  
