```pawn
stock NunnableHook() <endhook> {}
#define EndHook() state endhook

public OnGameModeInit() <>
{
	printf("Funcao OnGameModeInit 1");
	
	state _1;
	return OnGameModeInit();
}

public OnGameModeInit() <_1>
{
	printf("Funcao OnGameModeInit 2");
	
	state _2;
	return OnGameModeInit();
}

public OnGameModeInit() <_2>
{
	printf("Funcao OnGameModeInit 3");
	
	EndHook(); // indicar o ultimo gancho da funcao
	return 1; // cuidado para não criar um loop
}
```
**Resultado final:**
<p>Funcao OnGameModeInit 1</p>
<p>Funcao OnGameModeInit 2</p>
<p>Funcao OnGameModeInit 3</p>
