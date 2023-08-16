```pawn
new bool:pode_passar;

MudarLuz() <>
{
	print("Iniciando a simulação de um semáforo!");
	state Luz:Vermelho;
}

MudarLuz() <Luz:Vermelho>
{
	pode_passar = false;
	print("Semáforo está no vermelho!");
	
	state Luz:Amarelo;
}

MudarLuz() <Luz:Amarelo>
{
	print("Semáforo está no amarelo!");
	
	if(pode_passar)
		state Luz:Vermelho;
	else
		state Luz:Verde;
}

MudarLuz() <Luz:Verde>
{
	pode_passar = true;
	print("Semáforo está no verde!");
	
	state Luz:Amarelo;
}

forward RotateTrafficLight();
public RotateTrafficLight()
{
	MudarLuz();
	return 1;
}

main()
{
	SetTimer("RotateTrafficLight", 5000, 1);
	// Cada luz vai ter 5 segundos
}
```