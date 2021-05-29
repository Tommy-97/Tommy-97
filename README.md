package com.company;

import java.util.Scanner;

class Calculator {
    public static class Main {
        private static final char exitCharacter = '!';

        public static void main(String[] args) {
            DataReader reader = new DataReader(exitCharacter);
            while (true) {
                try {
                    reader.read();
                } catch (RuntimeException e) {
                    System.err.println(e.getMessage());
                    continue;
                }
                if (reader.isExitFlag()) {
                    System.out.println("В выражении пристутствует знак выхода: " + exitCharacter);
                    System.out.println("Завершение программы.");
                    break;
                }
                double result = Calculator1.calculate(reader.getVar1(), reader.getVar2(), reader.getOper());
                System.out.println(result);
            }
        }
    }


    public static class DataReader {

        private int number1;
        private int number2;
        private char operation;
        private boolean exitFlag;
        private final char exitCharacter;
        private final char resultChar;

        public DataReader(char exitCharacter) {
            this.exitCharacter = exitCharacter;
            this.resultChar = '=';
        }


        public void read() {

            Integer[] arabic = {10, 9, 8, 7, 6, 5, 4, 3, 2, 1};
            String[] roman = {"X", "IX", "VIII", "VII", "VI", "V", "IV", "III", "II", "I"};

            System.out.println("Введите выражение, состоящее из двух целых чисел от 0 до 10, знака операции и знака равно (напр. 2+2=): ");
            Scanner scanner = new Scanner(System.in);
            String text = scanner.nextLine();
            if (text.indexOf(exitCharacter) != -1) {
                exitFlag = true;
                return;
            }
