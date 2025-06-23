# dominio_rango_funcion.py
# Autor: [Tu nombre]
# Descripción: Calcula el dominio y rango de una función matemática usando SymPy

from sympy import symbols, S, sin, cos
from sympy.calculus.util import continuous_domain, function_range

# Definir la variable
x = symbols('x')

# 👉 Define aquí la función que quieres analizar
# Ejemplo 1: Polinómica
funcion = x**2 + 3*x + 2

# Ejemplo 2: Racional (descomenta si deseas probar)
# funcion = 1 / (x - 1)

# Ejemplo 3: Trigonométrica (descomenta si deseas probar)
# funcion = sin(x)

# Calcular el dominio (valores de x donde la función es continua)
dominio = continuous_domain(funcion, x, S.Reals)

# Calcular el rango (valores que toma la función)
rango = function_range(funcion, x, S.Reals)

# Mostrar resultados
print("🔍 Análisis de la función:")
print(f"Función: {funcion}")
print(f"📌 Dominio: {dominio}")
print(f"📌 Rango: {rango}")
