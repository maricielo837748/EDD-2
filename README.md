#include <iostream>
#include <string>
#include <vector> // Incluir la librería para vectores
using namespace std;

struct Persona {
    string nombre;
    int edad;
    Persona* padre;
    Persona* izquierda;
    Persona* derecha;
};

vector<Persona*> personas; // Declarar el vector

Persona* crearPersona(string nombre, int edad) {
    Persona* nueva = new Persona;
    nueva->nombre = nombre;
    nueva->edad = edad;
    nueva->padre = NULL;
    nueva->izquierda = NULL;
    nueva->derecha = NULL;
    personas.push_back(nueva);
    return nueva;
}

Persona* buscarPersona(string nombre) {
    for (int i = 0; i < personas.size(); i++) {
        if (personas[i]->nombre == nombre)
            return personas[i];
    }
    return NULL;
}

void agregarHijo(Persona* padre, Persona* hijo) {
    if (padre->izquierda == NULL) {
        padre->izquierda = hijo;
    } else if (padre->derecha == NULL) {
        padre->derecha = hijo;
    } else {
        cout << "El padre ya tiene dos hij@s.\n";
        return;
    }
    hijo->padre = padre;
}

void mostrarAncestros(Persona* persona) {
    if (persona->padre != NULL) {
        cout << persona->padre->nombre << " (" << persona->padre->edad << ")\n";
        mostrarAncestros(persona->padre);
    }
}

void mostrarDescendientes(Persona* persona) {
    if (persona != NULL) {
        if (persona->izquierda)
            cout << persona->izquierda->nombre << " (" << persona->izquierda->edad << ")\n";
        if (persona->derecha)
            cout << persona->derecha->nombre << " (" << persona->derecha->edad << ")\n";
        mostrarDescendientes(persona->izquierda);
        mostrarDescendientes(persona->derecha);
    }
}

void eliminarSubarbol(Persona* persona) {
    if (persona == NULL) return;

    eliminarSubarbol(persona->izquierda);
    eliminarSubarbol(persona->derecha);
    for (int i = 0; i < personas.size(); i++) {
        if (personas[i] == persona) {
            personas.erase(personas.begin() + i);
            break;
        }
    }
    delete persona;
}

void eliminarPersona(string nombre) {
    Persona* persona = buscarPersona(nombre);
    if (persona == NULL) {
        cout << "Persona no encontrada.\n";
        return;
    }

    if (persona->padre != NULL) {
        if (persona->padre->izquierda == persona)
            persona->padre->izquierda = NULL;
        else if (persona->padre->derecha == persona)
            persona->padre->derecha = NULL;
    }

    eliminarSubarbol(persona);
    cout << "Persona eliminada junto con sus descendientes.\n";
}

int obtenerOpcionValida() {
    int opcion;
    while (true) {
        cout << "Opcion: ";
        if (cin >> opcion) {
            if (opcion >= 1 && opcion <= 6) {
                cin.ignore(); // Limpiar el buffer(memori alamacenada)
                return opcion;
            } else {
                cout << "Por favor elija una opcion valida del menu (1-6)...\n";
            }
        } else {
            cout << "Entrada invalida. Por favor ingrese un numero del menu...\n";
            cin.clear(); // Limpiar el estado de error
            while (cin.get() != '\n'); // Limpia el buffer(memori alamacenada)
        }
    }
}

int obtenerEdadValida() {
    int edad;
    while (true) {
        cout << "Edad: ";
        if (cin >> edad) {
            if (edad >= 0) {
                cin.ignore(); // Limpiar el buffer(memori alamacenada)
                return edad;
            } else {
                cout << "La edad no puede ser negativa. Por favor ingrese un valor valido.\n";
            }
        } else {
            cout << "Entrada invalida. Por favor ingrese un numero valido.\n";
            cin.clear();
            while (cin.get() != '\n');
        }
    }
}

int main() {
    int opcion;
    string nombre, nombrePadre;
    int edad;
    Persona* raiz = NULL;
