"""Para hacer este desafio utilice emojis Unicode 
de https://emojipedia.org/ para ponerle un pocode onda
y tambien lo que yo llamo CSS Binarios(* y -) jaja"""
# Lista para guardar los productos. Cada producto será una sublista: [nombre, categoría, precio]
productos = []

# Variable para controlar el menú principal
opcion = ""

# Bucle principal del menú interactivo
while opcion != "5":
    # Mostrar el menú en pantalla
    print("************************************************************")
    print("\n📦 GESTOR DE PRODUCTOS 📦")                 
    print("1. Agregar producto")                          
    print("2. Ver productos")                             
    print("3. Buscar producto")                           
    print("4. Eliminar producto")                         
    print("5. Salir")                                     
    print("************************************************************")

    # Leer la opción del usuario
    opcion = input("Elegí una opción: ").strip()

    # Opción 1: Agregar producto
    if opcion == "1":
        # Pedir el nombre del producto, y validar que no esté vacío
        nombre = input("Nombre del producto: ").strip()
        while nombre == "":
            print("❌ El nombre no puede estar vacío.")
            nombre = input("Nombre del producto: ").strip()
        nombre = nombre.capitalize()  # <-- Aquí uso capitalize para formatear

        # Pedir la categoría del producto, y validar que no esté vacía
        categoria = input("Categoría del producto: ").strip()
        while categoria == "":
            print("❌ La categoría no puede estar vacía.")
            categoria = input("Categoría del producto: ").strip()
        categoria = categoria.capitalize()  # <-- Aquí también uso capitalize

        # Pedir el precio, validando que sea un número entero
        while True:
            precio_input = input("Precio (sin centavos): ").strip()
            if precio_input.isdigit():
                precio = int(precio_input)
                break
            else:
                print("❌ El precio debe ser un número entero sin centavos.")

        # Agregar el producto a la lista
        productos.append([nombre, categoria, precio])
        print("✅ Producto agregado correctamente.")

    # Opción 2: Ver todos los productos
    elif opcion == "2":
        # Verificar si la lista está vacía
        if len(productos) == 0:
            print("📭 No hay productos cargados.")
        else:
            print("\n📋 Lista de productos:")
            for i in range(len(productos)):
                # Mostrar cada producto con su número correspondiente
                print(f"{i + 1}. Nombre: {productos[i][0]}, Categoría: {productos[i][1]}, Precio: ${productos[i][2]}")

    # Opción 3: Buscar productos por nombre
    elif opcion == "3":
        # Leer el término de búsqueda
        termino = input("🔍 Ingresá el nombre o parte del nombre a buscar: ").strip().lower()  # .lower() ya estaba aquí
        encontrados = []

        # Buscar coincidencias en la lista de productos
        for p in productos:
            if termino in p[0].lower():
                encontrados.append(p)

        # Mostrar los productos encontrados o mensaje si no hay
        if len(encontrados) > 0:
            print("\n✅ Productos encontrados:")
            for p in encontrados:
                print(f"Nombre: {p[0]}, Categoría: {p[1]}, Precio: ${p[2]}")
        else:
            print("❌ No se encontraron productos con ese nombre.")

    # Opción 4: Eliminar productos por número
    elif opcion == "4":
        if len(productos) == 0:
            print("📭 No hay productos para eliminar.")
        else:
            # Mostrar la lista para elegir cuál eliminar
            print("\n📋 Lista de productos:")
            for i in range(len(productos)):
                print(f"{i + 1}. Nombre: {productos[i][0]}, Categoría: {productos[i][1]}, Precio: ${productos[i][2]}")

            # Intentar leer el número del producto a eliminar
            try:
                num = int(input("🗑️ Ingresá el número del producto que querés eliminar: "))
                if num >= 1 and num <= len(productos):
                    eliminado = productos.pop(num - 1)
                    print(f"✅ Producto '{eliminado[0]}' eliminado correctamente.")
                else:
                    print("❌ Número fuera de rango.")
            except ValueError:
                print("❌ Entrada inválida. Debe ser un número.")

    # Opción 5: Salir del programa
    elif opcion == "5":
        print("👋 ¡Gracias por usar el gestor de productos! Hasta luego.")

    # Si se ingresa una opción incorrecta
    else:
        print("❌ Opción inválida. Por favor, elegí una opción del 1 al 5.")
