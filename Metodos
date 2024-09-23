#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <float.h> // Para INFINITY

// Prototipos de función
void mostrarMenu();
double f(double x, int funcIndex);
void metodoDeBiseccion(double (*func)(double, int), double a, double b, int iteraciones, double tolerancia);
void secante(double a, double b, double epsilon, int imax, int funcIndex);

int main() {
    int op;
    do {
        mostrarMenu();
        printf("\n\tMenú de Métodos\n");
        printf("1 - Método de Bisección\n");
        printf("2 - Método de la Secante\n");
        printf("¿Qué método desea realizar?: ");
        scanf("%d", &op);
        system("pause");
        system("cls");

        if (op == 1) {
            int funcion, iteraciones;
            double a, b, tolerancia;

            printf("\n\tMenú de Funciones\n");
            printf("1 - f(x) = x^2 * cos(x) - 2x\n");
            printf("2 - f(x) = (6 - 2/x^2) * (exp(2+x)/4) + 1\n");
            printf("3 - f(x) = x^3 - 3 * sin(x^2) + 1\n");
            printf("4 - f(x) = x^3 + 6x^2 + 9.4x + 2.5\n");
            printf("¿Qué función desea calcular?\n");
            scanf("%d", &funcion);

            system("pause");
            system("cls");

            // Parámetros para el método de bisección
            printf("Ingrese los valores del intervalo:\n");
            printf("a: ");
            scanf("%lf", &a);

            printf("b: ");
            scanf("%lf", &b);

            printf("Máximo de iteraciones: ");
            scanf("%d", &iteraciones);

            printf("Tolerancia: ");
            scanf("%lf", &tolerancia);

            system("pause");
            system("cls");

            metodoDeBiseccion(f, a, b, iteraciones, tolerancia);
        } else if (op == 2) {
            double a, b, epsilon;
            int imax, funcIndex;

            printf("Seleccione la función a evaluar:\n");
            printf("1. f(x) = x^2 * cos(x) - 2x\n");
            printf("2. f(x) = (6 - 2 / (x * x)) * (exp(2 + x) / 4) + 1\n");
            printf("3. f(x) = x^3 - 3 * sin(x^2) + 1\n");
            printf("4. f(x) = x^3 + 6 * x^2 + 9.4 * x + 2.5\n");
            printf("Ingrese el número de la función: ");
            scanf("%d", &funcIndex);

            printf("Introduzca los límites del intervalo de búsqueda original, a y b: ");
            scanf("%lf %lf", &a, &b);
            printf("Introduzca el criterio de convergencia: ");
            scanf("%lf", &epsilon);
            printf("Introduzca el número máximo de iteraciones permitidas: ");
            scanf("%d", &imax);

            secante(a, b, epsilon, imax, funcIndex);
        } else {
            printf("Opción incorrecta\n");
        }

        printf("\nDesea: \nObtener otra raíz [1] \nRegresar al menú principal [0]\n");
        scanf("%d", &op);

        system("pause");
        system("cls");

    } while (op == 0);

    return 0;
}

// Esta función implementa el método de bisección
void metodoDeBiseccion(double (*func)(double, int), double a, double b, int iteraciones, double tolerancia) {
    double p, fp, fa, fb;
    int iter = 0;
    double Er = 1.0;

    printf("Iter\t a\t\t b\t\t p\t\t f(p)\t\t Error relativo\n");
    while (iter < iteraciones && Er > tolerancia) {
        p = (a + b) / 2.0;
        fa = func(a, 1);
        fb = func(b, 1);
        fp = func(p, 1);

        printf("%d\t %.6lf\t %.6lf\t %.6lf\t %.6lf\t %.6lf\n", iter + 1, a, b, p, fp, Er);

        if (iter > 0) {
            Er = fabs((b - a) / p);
        }

        if (fa * fp < 0) {
            b = p;
        } else {
            a = p;
        }
        iter++;
    }

    printf("\nLa raíz obtenida es: %.6lf\n", p);
    printf("Se alcanzó en la iteración: %d\n", iter);
    printf("Con una tolerancia de: %.6lf\n", Er);
}

// Esta función implementa el método de la secante
void secante(double a, double b, double epsilon, int imax, int funcIndex) {
    double x0 = a;
    double x1 = b;
    double f0 = f(x0, funcIndex);
    double f1 = f(x1, funcIndex);
    double x2, error;

    // Encabezado de la tabla
    printf("\nIter\t x0\t\t f(x0)\t\t x1\t\t f(x1)\t\t x2\t\t f(x2)\t\t Error\n");

    for (int i = 1; i <= imax; i++) {
        // Comprobar que no hay división por cero
        if (f1 - f0 == 0) {
            printf("Error: División por cero en la iteración %d.\n", i);
            return;
        }

        // Calcular la siguiente aproximación
        x2 = x1 - f1 * (x1 - x0) / (f1 - f0);
        double f2 = f(x2, funcIndex);
        error = fabs(f2);

        // Imprimir la fila de la tabla
        printf("%d\t %.10f\t %.10f\t %.10f\t %.10f\t %.10f\t %.10f\t %.10f\n", 
               i, x0, f0, x1, f1, x2, f2, error);

        // Verificar si se ha alcanzado la convergencia
        if (error < epsilon) {
            printf("Se encontró una raíz en x = %.10f\n", x2);
            printf("En %d iteraciones\n", i);
            printf("El valor de la función es %.10f\n", f2);
            return;
        }

        // Actualizar para la siguiente iteración
        x0 = x1;
        f0 = f1;
        x1 = x2;
        f1 = f2;
    }

    printf("Después de %d iteraciones, no se encontró ninguna raíz dentro del criterio de convergencia.\n", imax);
}

// Función para evaluar f(x) según el índice de función
double f(double x, int funcIndex) {
    switch (funcIndex) {
        case 1:
            return (x * x * cos(x) - 2 * x);
        case 2:
            if (x != 0)
                return (6 - 2 / (x * x)) * (exp(2 + x) / 4) + 1;
            else
                return INFINITY; // Para x=0, devolver infinito
        case 3:
            return (x * x * x - 3 * sin(x * x) + 1);
        case 4:
            return (x * x * x + 6 * x * x + 9.4 * x + 2.5);
        default:
            printf("Índice de función no válido.\n");
            return 0;
    }
}

// Función para mostrar el menú principal
void mostrarMenu() {
    printf("--------- Métodos Numéricos ----------\n");
    printf("------------ Integrantes -------------\n");
    printf("Mariana Alejandra López Ramírez\n");
    printf("Andrea Estephanie Fierro Ibáñez\n");
    printf("Jessica Esmeralda Alcantar Hernández\n");
}
