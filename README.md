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
