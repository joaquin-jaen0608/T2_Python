import random
import math

def generar_coordenadas(n):
    return [[random.randint(-81, 81), random.randint(-81, 81)] for _ in range(n)]

def distancia_origen(x, y):
    return math.sqrt(x ** 2 + y ** 2)

def mas_alejada(coordenadas):
    if not coordenadas:
        return None
    if len(coordenadas) == 1:
        x, y = coordenadas[0]
        if x > 0 and y < 0:
            return coordenadas[0]
        else:
            return None
    mid = len(coordenadas) // 2
    izquierda = mas_alejada(coordenadas[:mid])
    derecha = mas_alejada(coordenadas[mid:])

    def comparar(c1, c2):
        if not c1:
            return c2
        if not c2:
            return c1
        return c1 if distancia_origen(*c1) > distancia_origen(*c2) else c2

    return comparar(izquierda, derecha)

def main():
    n = int(input("¿Cuántos pares de coordenadas deseas generar?: "))
    coordenadas = generar_coordenadas(n)
    
    print("\nCoordenadas generadas:")
    for c in coordenadas:
        print(c)
    
    resultado = mas_alejada(coordenadas)
    if resultado:
        print(f"\nCoordenada más alejada del origen con X > 0 e Y < 0: {resultado}")
        print(f"Distancia desde el origen: {distancia_origen(*resultado):.2f}")
    else:
        print("\nNo hay coordenadas con X > 0 e Y < 0.")

if __name__ == "__main__":
    main()
