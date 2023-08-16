```pawn
stock __null <null>; // suprimir avisos/erros

public OnGameModeInit() <>
{
	print("Funcao OnGameModeInit 1");
	
	state GameModeInit:_1;
	return OnGameModeInit();
}

public OnGameModeInit() <GameModeInit:_1>
{
	print("Funcao OnGameModeInit 2");
	
	state GameModeInit:_2;
	return OnGameModeInit();
}

public OnGameModeInit() <GameModeInit:_2>
{
	print("Funcao OnGameModeInit 3");
	
	state null;
	return 1;
}

// não declare funções com o estado null
// pois ele serve apenas para que volte para a função sem estado
```