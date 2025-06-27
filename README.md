if (opcion == 1) {
            do {
                cout << "\nIngrese el nombre (o 0 para terminar de ingresar datos): ";
                getline(cin, nombre);
                
                if (nombre == "0") break;
                
                edad = obtenerEdadValida();
                
                Persona* nueva = crearPersona(nombre, edad);
                if (raiz == NULL) raiz = nueva;
                cout << "Persona registrada.\n";
                
            } while (true);
            
        } else if (opcion == 2) {
            cout << "Nombre del padre: ";
            getline(cin, nombrePadre);
            Persona* padre = buscarPersona(nombrePadre);
            if (!padre) {
                cout << "Padre no encontrado.\n";
                continue;
            }
            cout << "Nombre del hij@: ";
            getline(cin, nombre);
            Persona* hijo = buscarPersona(nombre);
            if (!hijo) {
                cout << "Hij@ no encontrado.\n";
                continue;
            }
            agregarHijo(padre, hijo);
        } else if (opcion == 3) {
            cout << "Nombre: ";
            getline(cin, nombre);
            Persona* persona = buscarPersona(nombre);
            if (!persona) cout << "No encontrada.\n";
            else mostrarAncestros(persona);
        } else if (opcion == 4) {
            cout << "Nombre: ";
            getline(cin, nombre);
            Persona* persona = buscarPersona(nombre);
            if (!persona) cout << "No encontrada.\n";
            else mostrarDescendientes(persona);
        } else if (opcion == 5) {
            cout << "Nombre de la persona a eliminar: ";
            getline(cin, nombre);
            eliminarPersona(nombre);
        }

    } while (opcion != 6);

    cout << "Cerrando el sistema.Hasta la proxima[Presionar enter]...\n";
    return 0;
}
