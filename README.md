# Tutorial de Uso da Diretiva State no Pawn

Neste tutorial, exploraremos em detalhes o uso da diretiva `state` na linguagem de programação Pawn. A diretiva `state` é uma característica poderosa que permite a criação de autômatos finitos para gerenciar o fluxo de controle em programas reativos e interativos. Vamos abordar todos os aspectos essenciais do uso dessa diretiva, incluindo exemplos de código, dicas de boas práticas e possíveis erros a serem evitados.

## Estados e Autômatos

Um estado, na linguagem Pawn, é um conjunto de funções que definem o comportamento do programa em resposta a eventos específicos. Cada estado pode ter suas próprias funções e configurações. Um autômato, por sua vez, é uma coleção de estados que representam um contexto ou uma máquina de estados.

## Declarar Estados

Aqui está como você pode declarar uma função com estado na linguagem Pawn:

```pawn
funcao() <MeuEstado>
{
	print("Funcao no MeuEstado");
}
```

## Declarar Autômatos e Associar Estados

Além de declarar estados, você também pode declarar autômatos e associar estados a eles. Veja como fazer isso:

```pawn
funcao() <MeuAutomato:EstadoA>
{
	print("Funcao no automato MeuAutomato estado EstadoA");
}
```

## Mudando de Estado

Você pode mudar de estado durante a execução do programa usando a diretiva `state`. Aqui está um exemplo de como fazer isso:

```pawn
funcao() <MeuEstado>
{
	print("Função no MeuEstado");
}

funcao() <MeuAutomato:EstadoA>
{
	print("Função no EstadoA do MeuAutomato");
}

main()
{
	state MeuEstado; // Mudança para o MeuEstado
	funcao(); // chamando funcao() do MeuEstado
	
	state MeuAutomato:EstadoB; // Mudança para o EstadoA do MeuAutomato
	funcao(); // chamando funcao() do EstadoA do MeuAutomato
}
```

## Entry Functions

Cada estado pode conter funções específicas que serão executadas quando o programa estiver nesse estado. As entry functions são executadas ao entrar em um estado:

```pawn
funcao() <MeuEstado>
{
	print("Funcao no MeuEstado");
}

entry() <MeuEstado>
{
	print("Entrando no MeuEstado");
}

main()
{
	print("Iniciando execucao");

	state MeuAutomato:EstadoA;
	Funcao();

	print("Finalizando execucao");
}
```

Como resultado obteremos a sequência de execução:

```
Iniciando execucao
Entrando no MeuEstado
Funcao no MeuEstado
Finalizando execucao
```

## State Condicional

A diretiva `state` também permite estados condicionais, que podem ser usados para criar fluxos de controle mais complexos. Isso é equivalente a usar `if` com a diretiva `state`. Veja o exemplo:

```pawn
new bool:condicao = true;
state (condicao) MeuEstadoCondicao;

// Isso será equivalente a: if(condicao) state MeuEstadoCondicao;
```

## Variáveis de Estado

Variáveis de estado permitem armazenar informações específicas de estado.

```pawn
new variavel<MeuAutomato:EstadoA;
new variavel<MeuAutomato:EstadoB;

entry() <MeuAutomato:EstadoA>
{
	variavel = 1; // MeuAutomato:EstadoA
}

funcao() <MeuAutomato:EstadoB>
{
	if (variavel == 1) // MeuAutomato:EstadoB
	{
		print("Variável de estado é 1");
	}
	else
	{
		print("Variável de estado não é 1");
	}
}
```

Como resultado obteremos: `Variável de estado não é 1`<br>
Afinal não mudamos o valor da variavel do `MeuAutomato:EstadoB`

## Múltiplos Estados e Autômatos em Funções e Variáveis

Você pode associar múltiplos estados e autômatos a uma única função ou variável, permitindo que elas respondam a diferentes contextos:

```pawn
funcao() <EstadoA, EstadoB>
{
	print("Funcao nos estados EstadoA e EstadoB");
}

new variavel<EstadoA, EstadoB>;
```

## Funções Sem Estados

Até agora, exploramos a associação de estados e autômatos a funções, o que permite que elas respondam a eventos específicos. No entanto, também é possível criar funções que não estão associadas a estados específicos. Essas funções são chamadas de "funções sem estados" e são declaradas usando a sintaxe `funcao() <>`.

```pawn
funcao() <>
{
	print("Funcao sem estados");
}
```

As funções sem estados podem ser chamadas quando não existe uma função com o estado atual. Elas são úteis para implementar lógica que não depende do contexto do estado.

## Evitando Erros Comuns

É importante evitar erros comuns ao trabalhar com estados:

- Certifique-se de que os estados sejam definidos corretamente antes de serem usados.
- Não tem como iniciar um estado ou automato com um numero, como solução utilize `_n`. Exemplo: `new myvar<MeuAutomato:_1>;`
- Evite duplicar estados em uma função. Exemplo:

```pawn
funcao() <MeuAutomato:EstadoA> {} // sem erro

funcao() <MeuAutomato:EstadoB> {} // sem erro

funcao() <MeuAutomato:EstadoA, MeuAutomato:EstadoB> {} // erro 021: simbolo ja definido: "funcao"
```

## Conclusão

A diretiva `state` no Pawn é uma ferramenta poderosa para modelar fluxos de controle complexos em programas reativos. Com autômatos e estados, você pode criar estruturas de programação mais organizadas e compreensíveis, facilitando a manutenção e o desenvolvimento de software. Lembre-se de seguir as melhores práticas e evitar erros comuns para aproveitar ao máximo essa funcionalidade.

Espero que este tutorial tenha esclarecido o uso da diretiva `state` no Pawn e inspire você a criar programas mais robustos e eficientes.

Este tutorial foi desenvolvido com base nas vagas informações do pawn-lang.pdf disponibilizado pela CompuPhase.<br>
Autoria de DeviceBlack 😁✌️

### Veja esses exemplos de uso

1. [Simulando um Semáforo](semaforo.md)
2. [Ganchos em Funções](hooking.md)