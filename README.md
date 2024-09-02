class Producto:
    def __init__(self, id_producto, nombre, cantidad, precio):
        self.id_producto = id_producto
        self.nombre = nombre
        self.cantidad = cantidad
        self.precio = precio

    def obtener_id(self):
        return self.id_producto

    def establecer_nombre(self, nombre):
        self.nombre = nombre

    def obtener_nombre(self):
        return self.nombre

    def establecer_cantidad(self, cantidad):
        self.cantidad = cantidad

    def obtener_cantidad(self):
        return self.cantidad

    def establecer_precio(self, precio):
        self.precio = precio

    def obtener_precio(self):
        return self.precio

    def __str__(self):
        return f"ID: {self.id_producto}, Nombre: {self.nombre}, Cantidad: {self.cantidad}, Precio: {self.precio}"
class Inventario:
    def __init__(self):
        self.productos = {}

    def añadir_producto(self, producto):
        if producto.obtener_id() in self.productos:
            print("El producto ya existe en el inventario.")
        else:
            self.productos[producto.obtener_id()] = producto
            print("Producto añadido.")

    def eliminar_producto(self, id_producto):
        if id_producto in self.productos:
            del self.productos[id_producto]
            print("Producto eliminado.")
        else:
            print("El producto no existe en el inventario.")

    def actualizar_producto(self, id_producto, cantidad=None, precio=None):
        if id_producto in self.productos:
            producto = self.productos[id_producto]
            if cantidad is not None:
                producto.establecer_cantidad(cantidad)
            if precio is not None:
                producto.establecer_precio(precio)
            print("Producto actualizado.")
        else:
            print("El producto no existe en el inventario.")

    def buscar_producto_por_nombre(self, nombre):
        for producto in self.productos.values():
            if producto.obtener_nombre() == nombre:
                print(producto)
                return producto
        print("Producto no encontrado.")
        return None
import pickle

def guardar_inventario(inventario, archivo):
    with open(archivo, 'wb') as f:
        pickle.dump(inventario.productos, f)
    print("Inventario guardado en el archivo.")

def cargar_inventario(archivo):
    inventario = Inventario()
    try:
        with open(archivo, 'rb') as f:
            inventario.productos = pickle.load(f)
        print("Inventario cargado desde el archivo.")
    except FileNotFoundError:
        print("Archivo no encontrado, se creará un inventario nuevo.")
    return inventario
def menu():
    inventario = cargar_inventario('inventario.pkl')
    while True:
        print("\n--- Sistema de Gestión de Inventario ---")
        print("1. Añadir producto")
        print("2. Eliminar producto")
        print("3. Actualizar producto")
        print("4. Buscar producto por nombre")
        print("5. Mostrar todos los productos")
        print("6. Guardar y salir")

        opcion = input("Seleccione una opción: ")

        if opcion == '1':
            id_producto = input("Ingrese el ID del producto: ")
            nombre = input("Ingrese el nombre del producto: ")
            cantidad = int(input("Ingrese la cantidad del producto: "))
            precio = float(input("Ingrese el precio del producto: "))
            producto = Producto(id_producto, nombre, cantidad, precio)
            inventario.añadir_producto(producto)
        elif opcion == '2':
            id_producto = input("Ingrese el ID del producto a eliminar: ")
            inventario.eliminar_producto(id_producto)
        elif opcion == '3':
            id_producto = input("Ingrese el ID del producto a actualizar: ")
            cantidad = input("Ingrese la nueva cantidad (dejar vacío si no desea cambiar): ")
            precio = input("Ingrese el nuevo precio (dejar vacío si no desea cambiar): ")
            cantidad = int(cantidad) if cantidad else None
            precio = float(precio) if precio else None
            inventario.actualizar_producto(id_producto, cantidad, precio)
        elif opcion == '4':
            nombre = input("Ingrese el nombre del producto a buscar: ")
            inventario.buscar_producto_por_nombre(nombre)
        elif opcion == '5':
            inventario.mostrar_todos_los_productos()
        elif opcion == '6':
            guardar_inventario(inventario, 'inventario.pkl')
            print("Saliendo del sistema...")
            break
        else:
            print("Opción no válida. Por favor, seleccione una opción del menú.")

if __name__ == "__main__":
    menu()

    def mostrar_todos_los_productos(self):
        if not self.productos:
            print("No hay productos en el inventario.")
        for producto in self.productos.values():
            print(producto)
