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
def menu_administrador() 
          while True:
        print("\n--- MENÚ DE ADMINISTRADOR ---")
        print("1. Agregar nuevo personaje")
        print("2. Listar personajes")
        print("3. Buscar personaje por nombre")
        print("4. Editar estilo de pelea")
        print("5. Eliminar personaje")
        print("6. Salir")
        op = int(input("Opción: "))
        if op == 1:
            nombreNuevo = input("Nombre del personaje: ")
            estilo = input("Estilo de pelea: ")
            habilidades = crear_arbol_habilidades()
            personajes[nombreNuevo] = {"estilo": estilo, "arbol": habilidades}
            print("Personaje agregado.")
        elif op == 2:
            if personajes:
                for p in personajes:
                    total = sumar_habilidades(personajes[p]["arbol"])
                    print(f"- {p}: {personajes[p]['estilo']} ({total} pts)")
            else:
                print("No hay personajes.")
        elif op == 3:
            nombreBuscar = input("Nombre a buscar: ")
            if nombreBuscar in personajes:
                print(f"{nombreBuscar} → Estilo: {personajes[nombreBuscar]['estilo']}")
                mostrar_arbol(personajes[nombreBuscar]["arbol"])
            else:
                print("No encontrado.")
        elif op == 4:
            estiloEditar = input("Nombre a editar: ")
            if estiloEditar in personajes:
                nuevoEstilo = input("Nuevo estilo de pelea: ")
                personajes[estiloEditar]["estilo"] = nuevoEstilo
                print("Estilo actualizado.")
            else:
                print("No encontrado.")
        elif op == 5:
            nombreEliminar = input("Nombre a eliminar: ")
            if nombreEliminar in personajes:
                del personajes[nombreEliminar]
                print("Personaje eliminado correctamente.")
            else:
                print("No existe")
        elif op == 6:
            break
        else:
            print("Opción inválida")
    

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
