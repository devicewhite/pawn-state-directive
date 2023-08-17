```pawn
stock NunnableHook() <_0> {}; // suprimir avisos/erros
#define EndHook() state _0

public OnGameModeInit() <>
{
	print("Funcao OnGameModeInit 1");
	
	state GameModeInit:_1;
	return OnGameModeInit();
}

public OnGameModeInit() <GameModeInit:_1>
{
	print("Funcao OnGameModeInit 2");
	
	state _2;
	return OnGameModeInit();
}

public OnGameModeInit() <GameModeInit:_2>
{
	print("Funcao OnGameModeInit 3");
	
	EndHook();
	return 1;
}

// não declare funções com o estado _0
// pois ele serve apenas para que volte para a função sem estado
```