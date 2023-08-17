```pawn
stock NunnableHook() <endhook> {};
#define EndHook() state endhook

public OnGameModeInit() <>
{
	print("Funcao OnGameModeInit 1");
	
	state _1;
	return OnGameModeInit();
}

public OnGameModeInit() <_1>
{
	print("Funcao OnGameModeInit 2");
	
	state _2;
	return OnGameModeInit();
}

public OnGameModeInit() <_2>
{
	print("Funcao OnGameModeInit 3");
	
	EndHook();
	return 1; // cuidado para não criar um loop
}
```