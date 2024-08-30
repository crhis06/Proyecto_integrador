# Proyecto_integrador
# Descripción
Este código creado en Python implementa un sistema básico de autenticación de usuarios que permite a los usuarios iniciar sesión proporcionando un nombre de usuario y una contraseña. Utiliza el algoritmo de hash SHA-256 para almacenar y verificar contraseñas de forma segura.

# Funcionalidades Principales
Hashing de Contraseñas: Genera un hash seguro para contraseñas usando el algoritmo SHA-256.

Verificación de Contraseñas: Verifica si la contraseña proporcionada coincide con el hash almacenado.

Gestión de Intentos de Inicio de Sesión: Limita el número de intentos de inicio de sesión a un máximo predefinido para mejorar la seguridad.

Diccionario de Usuarios: Utiliza un diccionario para almacenar los nombres de usuario y sus contraseñas hasheadas.

# Cómo Funciona
Hash de Contraseñas: La función hash_password(password) toma una contraseña en texto plano, la codifica y genera un hash SHA-256.

Verificación de Contraseñas: La función verify_password(stored_hash, password) compara el hash de la contraseña proporcionada con el hash almacenado para verificar su validez.

# Proceso de Inicio de Sesión:

El usuario debe ingresar su nombre de usuario y contraseña.
El sistema verifica la combinación de usuario y contraseña.
Se permite un número limitado de intentos para ingresar la contraseña correctamente.
Si el inicio de sesión es exitoso, el sistema muestra un mensaje de bienvenida.
Si se agotan los intentos, el usuario recibe un mensaje indicando que debe intentar más tarde.
# Código
import hashlib

# Función para hash de contraseñas
def hash_password(password):
    """Genera un hash seguro para la contraseña."""
    return hashlib.sha256(password.encode()).hexdigest()

# Función para verificar la contraseña
def verify_password(stored_hash, password):
    """Verifica si la contraseña proporcionada coincide con el hash almacenado."""
    return stored_hash == hash_password(password)

# Diccionario de usuarios y contraseñas (hash)
users = {
    "Crhis06": hash_password("12345@")
}

# Número máximo de intentos
max_intentos = 3

# Bucle para manejar múltiples intentos de inicio de sesión
for intento in range(max_intentos):
    print("Bienvenido, ingresa tu usuario")
    user = input("Usuario: ")

    print("Contraseña: ")
    pwd = input()

    if user in users and verify_password(users[user], pwd):
        print("Bienvenido de vuelta", user)
        break  # Salir del bucle si el inicio de sesión es exitoso
    else:
        print("Usuario o contraseña incorrectos")
        if intento < max_intentos - 1:
            print("Tienes", max_intentos - (intento + 1), "intentos restantes")
        else:
            print("Has agotado el número máximo de intentos. Por favor, intenta más tarde.")

# Este bloque se ejecuta después de salir del bucle
print("Fin del proceso de inicio de sesión.")
