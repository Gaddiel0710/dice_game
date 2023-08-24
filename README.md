# DICE_GAME
## _dice game in which two players must try to get the target number_

Objective: The game consists of players rolling a die to determine a target, then rolling two dies each and scoring points if they roll the value of the target. At the end of each match,
the winner of that match is displayed. The game can be played multiple times and a full summary of the games and the clear winner is shown at the end.

## libraries used

```python
import os
import time as ti
import msvcrt as ms
import random as ra
```

## Principal function

_This is the main function of the game, which runs the entire game process._

```python
def main():
    os.system('cls')
    for i in range(1,5):
        print("==JUEGO DE DADOS==")
        time.sleep(1/4)
        os.system('cls')
        time.sleep(1/4)    
    print("==JUEGO DE DADOS==\n")
    time.sleep(1/2)
    print("""INSTRUCCIONES:
1.- Se necesitan 2 jugadores
2.- Se tiraran un dado para dictar el objetivo
3.- Cada jugador realizara un tiro de forma alternada
4.- Se sumara un punto al jugador que obtenga un numero igual al objetivo """)
    time.sleep(3/2)
    print("Presione enter para continuar...")
    msvcrt.getch()
    os.system('cls')
    GZF_players = jugadores()
    GZF_matriz_juego=[]
    GZF_victorias=[0,0,0,0]
    GZF_registro_victorias=[]
    GZF_num_Juegos=1
    while True:
        os.system("cls")
        GZF_partida=[]
        for t in range (3, 0,-1):
            print("Cargando partida numero ",GZF_num_Juegos,"...", t)
            time.sleep(1)
            os.system("cls")
        GZF_objetivo=random.randint(1,6)
        GZF_partida.append(GZF_objetivo)
        GZF_tiros=tiros(GZF_players,GZF_objetivo)          
        GZF_partida.extend(GZF_tiros)
        GZF_registro_victorias=ganadas(GZF_victorias,GZF_partida[5],GZF_partida[6])
        GZF_matriz_juego.append(GZF_partida)
        GZF_otro_juego=volver_a_jugar()   
        if GZF_otro_juego==0:
            resumen(GZF_matriz_juego,GZF_registro_victorias,GZF_num_Juegos,GZF_players)
            break
        GZF_num_Juegos+=1
   
if __name__ == "__main__":
    main()
```

## Function players

_This function asks users to enter the names of the players and returns a list of their names._

```python
def jugadores():
    print("Ingresen el nombre de los jugadores\n")
    GZF_players=[]
    GZF_player1 = (str(input("Ingrese el nombre del primer jugador: "))).upper()
    os.system('cls')
    GZF_players.append(GZF_player1)
    GZF_player2 = (str(input("Ingrese el nombre del segundo jugador: "))).upper()
    os.system('cls')
    GZF_players.append(GZF_player2)    
    return (GZF_players)
```

## function adds or does not add

_This function checks if the value of the shot is equal to the target and returns 1 if so (meaning the player scores a point) or 0 if not equal (the player scores nothing)._

```python
def suma_no_suma(tiro,objetivo):
    GZF_punto=0
    if tiro==objetivo:
        GZF_punto=1
        print("Sumas un punto :)")
    else:
        print("No sumas nada :(")
    return GZF_punto
```

## match winner

_This function determines who won the match between the players and returns the results._

```python
def winner_de_partida(player1_puntos,player2_puntos,jugadores):
    GZF_resultados=[player1_puntos,player2_puntos]
    print("******************Resultados de partida******************* ")
    print("El jugador ",jugadores[0]," obtuvo ", player1_puntos," puntos")
    print("El jugador ",jugadores[1]," obtuvo ", player2_puntos," puntos")
    time.sleep(1/2)
    if player1_puntos==0 and player2_puntos==0:
        print("Nadie obtuvo puntos,Gano la maquina")
        time.sleep(1/4)
        GZF_resultados.append("Maquina")
    elif player1_puntos>player2_puntos:
        print("Felicidades jugador ", jugadores[0]," usted gano la partida")
        time.sleep(1/4)
        GZF_resultados.append(jugadores[0])
    elif player2_puntos>player1_puntos:
        print("Felicidades jugador ", jugadores[1]," usted gano la partida")
        time.sleep(1/4)
        GZF_resultados.append(jugadores[1])
    elif player1_puntos==player2_puntos:
        print("Partida Empatada: El jugador ", jugadores[0], " y el jugador ", jugadores[1]," obtuvieron los mismo puntos")
        time.sleep(1/4)
        GZF_resultados.append("Empate")
    print("\nPresiona enter para continuar...")
    msvcrt.getch()
    os.system('cls')
    return GZF_resultados
```

## function shooting

_This function handles player rolls, generates random numbers for the dice rolls, and calculates the points scored by each player._

```python
def tiros(jugadores,objetivo):
    GZF_player1_points=0
    GZF_player2_points=0
    GZF_tiros_partida=[]
    for i in range (1,3):
        os.system("cls")
        print("El objetivo de la partida es: ",objetivo)
        print("Jugador ", jugadores[0], " presione enter para realizar  tu tiro num.", i)
        msvcrt.getch()
        GZF_tiro_p1=random.randint(1,6) 
        GZF_tiros_partida.append(GZF_tiro_p1)
        print("Obtuviste", GZF_tiro_p1)
        GZF_player1_points+=suma_no_suma(GZF_tiro_p1,objetivo) 
        print("Presione enter para siguiente jugador...")
        msvcrt.getch()
        os.system("cls")
        print("El numero objetivo es: ", objetivo)
        print("Jugador ", jugadores[1], "presione enter para realizar  tu tiro num.", i)
        msvcrt.getch()
        GZF_tiro_p2=random.randint(1,6) 
        GZF_tiros_partida.append(GZF_tiro_p2) 
        print("Obtuviste", GZF_tiro_p2)
        GZF_player2_points+=suma_no_suma(GZF_tiro_p2,objetivo) 
        if i == 2:
            print("Presiona enter continuar...")
        else:
            print("Presione enter para siguiente jugador...")
        msvcrt.getch()
    os.system("cls")
    GZF_win_partida=winner_de_partida(GZF_player1_points,GZF_player2_points,jugadores)
    GZF_tiros_partida.extend(GZF_win_partida)
    return GZF_tiros_partida
```

## Function victories

_This feature updates the win record based on the match result._

```python
def ganadas(victorias,player1_points,player2_points):
    if player1_points>player2_points:
        GZF_SumaPuntos=victorias[0]
        GZF_SumaPuntos+=1
        victorias[0]=GZF_SumaPuntos
    elif player2_points>player1_points:
        GZF_SumaPuntos=victorias[1]
        GZF_SumaPuntos+=1
        victorias[1]=GZF_SumaPuntos        
    elif player1_points==0 and player2_points==0:
        GZF_SumaPuntos=victorias[2]
        GZF_SumaPuntos+=1
        victorias[2]=GZF_SumaPuntos
    elif player1_points==player2_points:
        GZF_SumaPuntos=victorias[3]
        GZF_SumaPuntos+=1
        victorias[3]=GZF_SumaPuntos
    return victorias
```

## function play another round

_This function asks the user if they want to play again and returns a decision based on their answer._

```python
def volver_a_jugar():
    GZF_desicion=1
    while True:
        os.system("cls")
        GZF_otro_juego=input("¿Jugar de nuevo? S/N ")
        if GZF_otro_juego.upper()=="S":              
            GZF_desicion=1
            break
        elif GZF_otro_juego.upper()=="N":
            GZF_desicion=0
            break
        else:
            print("la desicion ingresada no es valida por favor intente de nuevo")
            time.sleep(1)
            os.system('cls')
    return GZF_desicion
```

## undisputed champion function

_This feature determines the outright winner based on the win record._

```python
def indiscutible(players, registro_victorias):
    GZF_winners = []
    GZF_puntos_maximos = 0
    GZF_winner_indiscutible = " "
    for i in registro_victorias:
        if i > GZF_puntos_maximos:
            GZF_puntos_maximos = i
    for j in registro_victorias:
        if GZF_puntos_maximos== j:
            GZF_winners.append(j)    
    if len(GZF_winners) == 1:
        if GZF_puntos_maximos == registro_victorias[0]:
            GZF_winner_indiscutible = players[0]
        elif GZF_puntos_maximos == registro_victorias[1]:
            GZF_winner_indiscutible = players[1]
        elif GZF_puntos_maximos == registro_victorias[2]:
            GZF_winner_indiscutible = "La Máquina"
    elif len(GZF_winners) == 2:
        GZF_winner_indiscutible = "No hay ganador indiscutible, Empate entre los 2 jugadores"
    else:
        GZF_winner_indiscutible = "No hay ganador indiscutible, Empate entre los 2 jugadores"  
    return GZF_winner_indiscutible
```

## summary function

_This function shows a detailed summary of the games played, the results and the undisputed winner._

```python
def resumen(GZF_matriz_juego,GZF_registro_victorias,GZF_num_Juegos,GZF_players):
    os.system("cls")
    print("Resumen de los encuentros por partida:")
    print("el numero de juegos realizados es: ", GZF_num_Juegos)
    for i in range (GZF_num_Juegos):
        print("**************************************************************************")
        print("juego numero ", i+1)
        print("El objetivo fue: ", GZF_matriz_juego[i][0])
        print("En su primer tiro, el jugador ", GZF_players[0], " obtuvo: ", GZF_matriz_juego[i][1]," en el dado lanzado")
        print("En su primer tiro, el jugador ", GZF_players[1], "obtuvo: ", GZF_matriz_juego[i][2]," en el dado lanzado")
        print("En su segundo tiro, el jugador", GZF_players[0], "obtuvo: ", GZF_matriz_juego[i][3]," en el dado lanzado")
        print("En su segundo tiro, el jugador", GZF_players[1], "obtuvo: ",GZF_matriz_juego[i][4]," en el dado lanzado")
        print("El total de los puntos obtenidos por ",GZF_players[0], " fueron: ", GZF_matriz_juego[i][5])
        print("El total de los puntos obtenidos por ", GZF_players[1], "fueron: ", GZF_matriz_juego[i][6])
        print("El ganador del juego ", i+1, "fue: ", GZF_matriz_juego[i][7])
        print("***************************************************************************")
        print(" ")
    print("Presiona enter para continuar...")
    msvcrt.getch()
    os.system("cls")
    print("REGISTRO TOTAL DE VICTORIAS\n")
    print("Numero de juegos realizados:", GZF_num_Juegos)
    print()
    print("El jugador ",GZF_players[0]," obtuvo la victoria en: ", GZF_registro_victorias[0]," juegos")
    print("El jugador ",GZF_players[1]," obtuvo la victoria en: ", GZF_registro_victorias[1]," juegos")
    print("La maquina obtuvo la victoria en: ", GZF_registro_victorias[2]," juegos")
    print("Y se obtuvieron empates en: ", GZF_registro_victorias[3]," juegos")

    GZF_indiscutible = indiscutible(GZF_players, GZF_registro_victorias)
    print("******************************************************************")
    if GZF_indiscutible != "No hay ganador indiscutible, Empate entre los 2 jugadores":
        print("El ganador indiscutible con más puntos totales fue:", GZF_indiscutible)
    else:
        print(GZF_indiscutible)
    print("******************************************************************")
    print("\nPresiona enter para continuar...")
    msvcrt.getch()
    os.system("cls")
    for t in range (3, 0,-1):
        print("terminado juego... ", t)
        time.sleep(1/2)
        os.system("cls")
    for i in range(1,3):
        print("GAME OVER")
        time.sleep(1/2)
        os.system("cls")
    print("¡GRACIAS POR JUGAR!")
    print("Hasta la proxima gamers")
    time.sleep(2)
```
