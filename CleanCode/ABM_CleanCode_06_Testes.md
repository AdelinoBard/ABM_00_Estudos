# **Testes em C#**

Em C#, assim como preconiza o "Código Limpo", testes automatizados são mais cruciais que a entrega inicial do código. Se você não possui uma suíte de testes robusta, ou se a cobertura é inadequada, cada nova implantação se torna uma fonte potencial de regressões e incertezas. Definir o que constitui uma cobertura "adequada" é uma decisão da equipe, mas almejar 100% de cobertura de linhas e branches é o caminho para alcançar alta confiança e tranquilidade no desenvolvimento. Para isso, além de um excelente *framework* de testes, integrar uma boa ferramenta de análise de cobertura de código é fundamental.

Não há justificativa para negligenciar a escrita de testes em C#. O ecossistema .NET oferece diversos *frameworks* de testes poderosos, como **xUnit.net**, **NUnit** e **MSTest**. Explore as opções e escolha aquele que melhor se adapta às necessidades e preferências da sua equipe. Uma vez definido o *framework*, o objetivo deve ser escrever testes para cada nova funcionalidade ou módulo introduzido. Adotar o Desenvolvimento Orientado a Testes (TDD) é uma prática valiosa, mas o ponto essencial é garantir que as metas de cobertura sejam atingidas antes de qualquer lançamento ou refatoração significativa.

## Um Conceito por Teste (C#)

A clareza e o foco são essenciais em testes unitários. Cada teste deve verificar um único aspecto do comportamento da unidade sob teste. Isso facilita a identificação da causa de uma falha e torna os testes mais fáceis de entender e manter.

**Ruim (C#):**

```csharp
using Microsoft.VisualStudio.TestTools.UnitTesting;
using System;

[TestClass]
public class DateHelperTests
{
    [TestMethod]
    public void ManipulaLimitesDeDatas()
    {
        var date = new DateTime(2015, 1, 1);
        DateHelper.AddDays(ref date, 30);
        Assert.AreEqual(new DateTime(2015, 1, 31), date);

        date = new DateTime(2016, 2, 1);
        DateHelper.AddDays(ref date, 28);
        Assert.AreEqual(new DateTime(2016, 2, 29), date);

        date = new DateTime(2015, 2, 1);
        DateHelper.AddDays(ref date, 28);
        Assert.AreEqual(new DateTime(2015, 3, 1), date);
    }
}
```

**Bom (C#):**

```csharp
using Microsoft.VisualStudio.TestTools.UnitTesting;
using System;

[TestClass]
public class DateHelperTests
{
    [TestMethod]
    public void Adicionar30DiasEmJaneiro()
    {
        var date = new DateTime(2015, 1, 1);
        DateHelper.AddDays(ref date, 30);
        Assert.AreEqual(new DateTime(2015, 1, 31), date);
    }

    [TestMethod]
    public void AdicionarDiasEmAnoBissextoFevereiro()
    {
        var date = new DateTime(2016, 2, 1);
        DateHelper.AddDays(ref date, 28);
        Assert.AreEqual(new DateTime(2016, 2, 29), date);
    }

    [TestMethod]
    public void AdicionarDiasEmAnoNaoBissextoFevereiro()
    {
        var date = new DateTime(2015, 2, 1);
        DateHelper.AddDays(ref date, 28);
        Assert.AreEqual(new DateTime(2015, 3, 1), date);
    }
}
```

---