# ahorcado

package com.mantilla;

import java.util.Random;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        String palabraSecreta = getPalabraSecreta();
        char[] palabraGuiones = getGuionesFromPalabra(palabraSecreta);
        boolean juegoTerminado = false;
        int errores = 0;
        int maxErrores = 3;
        Scanner lector = new Scanner(System.in);

        while (!juegoTerminado) {
            System.out.println("Introduce una letra:");
            char letra = lector.next().charAt(0);
            boolean algunaLetraAcertada = false;

            for (int i = 0; i < palabraSecreta.length(); i++) {
                if (palabraSecreta.charAt(i) == letra) {
                    palabraGuiones[i] = letra;
                    algunaLetraAcertada = true;
                }
            }

            if (!algunaLetraAcertada) {
                errores++;
                System.out.println("Letra incorrecta, intenta nuevamente. Intentos restantes: " + (maxErrores - errores));
            }

            System.out.println(palabraGuiones);

            // Verificar si el juego ha terminado
            juegoTerminado = true;
            for (int i = 0; i < palabraGuiones.length; i++) {
                if (palabraGuiones[i] == '_') {
                    juegoTerminado = false;
                    break;
                }
            }

            if (errores >= maxErrores) {
                juegoTerminado = true;
                System.out.println("¡A mimir por siempre!!!");
            }
        }

        if (errores < maxErrores) {
            System.out.println("¡Felicidades! Has adivinado la palabra: " + palabraSecreta);
        }
    }

    static String getPalabraSecreta() {
        String[] palabras = {"casa", "perro", "gato", "caneca", "automovil"};
        Random random = new Random();
        int n = random.nextInt(palabras.length);
        return palabras[n];
    }

    static char[] getGuionesFromPalabra(String palabra) {
        int nPalabraSecreta = palabra.length();
        char[] palabraGuiones = new char[nPalabraSecreta];
        for (int i = 0; i < palabraGuiones.length; i++) {
            palabraGuiones[i] = '_';
        }
        return palabraGuiones;
    }
}
