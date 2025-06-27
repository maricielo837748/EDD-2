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
