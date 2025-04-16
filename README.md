Claro! Aqui está a versão atualizada e mais profissional, com exemplos realistas de saída do terminal usando **cores e indicações de sucesso ou falha**, como geralmente aparecem ao rodar `dotnet test`. Essa adição mostra de forma clara como o desenvolvedor pode identificar resultados esperados e valores reais em caso de erro:

---

## 🧪 Projeto de Testes - IMC com xUnit (.NET)

Este repositório apresenta um módulo de testes automatizados utilizando o framework **xUnit** com a plataforma **.NET**, aplicado à validação de uma classe responsável pelo cálculo e classificação do IMC (Índice de Massa Corporal).

---

### ✅ Estrutura dos Testes

Foram implementados dois tipos principais de testes com base nos atributos do xUnit:

#### `[Fact]`
Utilizado para validar cenários únicos e bem definidos.  
No projeto, é aplicado para verificar se o cálculo do IMC está correto para um determinado conjunto de entrada.

```csharp
[Fact]
public void Teste_Calculo_IMC()
{
    double imc_previsto = 31.25;
    IMC i = new IMC();
    i.peso = 80;
    i.altura = 1.60;
    i.Calcular_IMC();
    Assert.Equal(imc_previsto, i.imc);
}
```

#### `[Theory]`
Indicado para testes com múltiplos conjuntos de dados.  
Neste caso, é utilizado para verificar se a classificação do IMC corresponde corretamente ao valor calculado.

```csharp
[Theory]
[InlineData("Abaixo do peso")]
[InlineData("Peso normal")]
[InlineData("Sobrepeso")]
[InlineData("Obesidade Grau I")]
[InlineData("Obesidade Grau II")]
[InlineData("Obesidade Grau III")]
public void Teste_Categoria_IMC(string cat)
{
    IMC i = new IMC();
    i.peso = 80;
    i.altura = 1.60;
    i.Calcular_IMC();
    i.Classificar_IMC();
    Assert.Equal(i.categoria, cat);
}
```

> ⚠️ **Importante**: todos os testes acima usam os mesmos valores de peso e altura. Para uma validação mais completa, recomenda-se parametrizar os testes com diferentes combinações de dados para cobrir todas as categorias corretamente.

---

### 🖥️ Exemplo de Saída no Terminal

#### ✅ Teste com sucesso:

```bash
Passed Teste_Calculo_IMC [1 ms]
Passed Teste_Categoria_IMC("Obesidade Grau I") [2 ms]
```

#### ❌ Teste com falha:

```bash
Failed Teste_Categoria_IMC("Peso normal") [3 ms]
  Assert.Equal() Failure
  Expected: Peso normal
  Actual:   Obesidade Grau I
  Stack Trace:
     at atividade_imc_xunit.UnitTest1.Teste_Categoria_IMC(String cat) in C:\Testes\UnitTest1.cs:line 26
```

Nesse exemplo, o teste esperava a categoria `"Peso normal"`, mas a classificação real calculada foi `"Obesidade Grau I"` — indicando que os dados de entrada precisam ser ajustados para representar corretamente a categoria esperada.

---

### 🛠 Tecnologias Utilizadas

- [.NET](https://dotnet.microsoft.com/)
- [C#](https://learn.microsoft.com/dotnet/csharp/)
- [xUnit](https://xunit.net/)

---

### ▶️ Como Executar

Siga os passos abaixo para compilar e rodar os testes localmente:

1. Abra o terminal na raiz do projeto.

2. Restaure os pacotes do projeto (se necessário):
   ```bash
   dotnet restore
   ```

3. Compile a solução:
   ```bash
   dotnet build
   ```

4. Execute os testes:
   ```bash
   dotnet test
   ```

Os testes executados mostrarão no terminal quais passaram e quais falharam, com mensagens detalhadas sobre os valores esperados e os valores reais.

---

Se quiser, posso salvar esse conteúdo direto num arquivo `README.md`. É só avisar!