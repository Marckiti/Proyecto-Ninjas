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
