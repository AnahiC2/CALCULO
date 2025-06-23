# dominio_rango.py
# Autor: [Tu nombre]
# Descripción: Calcula el dominio y rango de funciones matemáticas simples usando SymPy

from sympy import symbols, solve, S, Interval, Union, oo
from sympy.calculus.util import continuous_domain, function_range
from sympy.functions import sin, cos
from sympy.abc import x

def calcular_dominio(funcion):
    """
    Calcula el dominio de una función simbólica usando SymPy.
    """
    dominio = continuous_domain(funcion, x, S.Reals)
    return dominio

def calcular_rango(funcion):
    """
    Calcula una aproximación del rango de una función simbólica.
    """
    try:
        rango = function_range(funcion, x, S.Reals)
        return rango
    except Exception as e:
        return f"No se pudo calcular el rango: {e}"

def mostrar_resultados(funcion):
    """
    Imprime la función, su dominio y su rango.
    """
    print(f"Función: {funcion}")
    dominio = calcular_dominio(funcion)
    print(f"Dominio: {dominio}")
    rango = calcular_rango(funcion)
    print(f"Rango: {rango}")

# Ejemplos de funciones
if __name__ == "__main__":
    funciones = [
        x**2 - 3*x + 2,         # Polinómica
        1 / (x - 2),            # Racional
        sin(x),                # Trigonométrica
        1 / (x**2 + 1)         # Función racional continua
    ]

    for f in funciones:
        print("-" * 40)
        mostrar_resultados(f)
