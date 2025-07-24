import random
from collections import deque


class NodoHabilidad:
    def __init__(self, nombre, puntos):
        self.nombre = nombre
        self.puntos = puntos
        self.izquierda = None
        self.derecha = None

def crear_arbol_habilidades():
    raiz = NodoHabilidad("rasengan", random.randint(5, 10))
    raiz.izquierda = NodoHabilidad("chidori", random.randint(5, 10))
    raiz.derecha = NodoHabilidad("amaterasu", random.randint(5, 10))
    raiz.izquierda.izquierda = NodoHabilidad("jutsu clones de sombra", random.randint(5, 10))
    raiz.derecha.derecha = NodoHabilidad("edo tensei", random.randint(5, 10))
    return raiz

def sumar_habilidades(nodo):
    if nodo is None:
        return 0
    return nodo.puntos + sumar_habilidades(nodo.izquierda) + sumar_habilidades(nodo.derecha)

def mostrar_arbol(nodo, nivel=0):
    if nodo:
        print(" " * nivel + f"{nodo.nombre} ({nodo.puntos})")
        mostrar_arbol(nodo.izquierda, nivel + 2)
        mostrar_arbol(nodo.derecha, nivel + 2)

personajes = {"Hajime Saitō","Himura Kenshin"}
def login_admin():
    print("===LOGIN ADMINISTRADOR===")
    while True:
        adminUsuario=input("Usuario: ")
        adminContra=input("Contrasena: ")
        if adminUsuario=="ADMINARUTO" and adminContra=="NARUTO123":
            print("Acceso concedido.")
            break
    menu_administrador() 
    # SIMULACION DE TORNEO E INICIALIZACION (JOSHUA CARLOSAMA)
    def simular_torneo():
    participantes = list(personajes.keys())
    ronda = 1
    while len(participantes) > 1:
        print(f"\n🏁 Ronda {ronda} - {len(participantes)} participantes")
        random.shuffle(participantes)
        nueva_ronda = []
        while len(participantes) > 1:
            p1 = participantes.pop()
            p2 = participantes.pop()
            h1 = sumar_habilidades(personajes[p1]["arbol"])
            h2 = sumar_habilidades(personajes[p2]["arbol"])
            ganador = p1 if h1 >= h2 else p2
            print(f"{p1} ({h1}) vs {p2} ({h2}) → Gana {ganador}")
            nueva_ronda.append(ganador)
        if participantes:
            solitario = participantes.pop()
            print(f"{solitario} pasa automáticamente")
            nueva_ronda.append(solitario)
        participantes = nueva_ronda
        ronda += 1
    print(f"\n👑 Campeón del torneo: {participantes[0]}")

def main():
    while True:
        print("\n=== SISTEMA DE PELEAS SAMURAI X ===")
        print("1. Ingresar como ADMIN")
        print("2. Ingresar como CLIENTE")
        print("3. Salir")
        op = input("Elige una opción: ")
        if op == "1":
            login_admin()
        elif op == "2":
            menu_cliente()
        elif op == "3":
            print("¡Hasta pronto Samurai!")
            break
        else:
            print("Opción inválida.")

main()
