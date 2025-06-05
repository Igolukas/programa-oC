#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>

#define TOTAL_CARTAS 5

typedef struct {
    char nome[30];
    int forca;
    int velocidade;
    int inteligencia;
} Carta;

// Função para imprimir os atributos da carta
void mostrarCarta(Carta c) {
    printf("Carta: %s\n", c.nome);
    printf("1. Força: %d\n", c.forca);
    printf("2. Velocidade: %d\n", c.velocidade);
    printf("3. Inteligência: %d\n", c.inteligencia);
}

// Função para comparar cartas
void comparar(Carta jogador, Carta computador, int atributo) {
    int valJogador, valComputador;

    switch (atributo) {
        case 1:
            valJogador = jogador.forca;
            valComputador = computador.forca;
            break;
        case 2:
            valJogador = jogador.velocidade;
            valComputador = computador.velocidade;
            break;
        case 3:
            valJogador = jogador.inteligencia;
            valComputador = computador.inteligencia;
            break;
        default:
            printf("Atributo inválido.\n");
            return;
    }

    printf("\nSua carta:\n");
    mostrarCarta(jogador);
    printf("\nCarta do computador:\n");
    mostrarCarta(computador);

    printf("\nResultado: ");
    if (valJogador > valComputador) {
        printf("Você venceu!\n");
    } else if (valJogador < valComputador) {
        printf("O computador venceu.\n");
    } else {
        printf("Empate!\n");
    }
}

int main() {
    srand(time(NULL));

    // Base de cartas
    Carta baralho[TOTAL_CARTAS] = {
        {"Dragão Flamejante", 90, 60, 40},
        {"Ciborgue Veloz", 50, 95, 70},
        {"Mago Ancião", 40, 55, 100},
        {"Guerreiro Orc", 85, 45, 30},
        {"Alienígena X", 60, 70, 85}
    };

    // Sorteia carta para jogador e computador
    int idxJogador = rand() % TOTAL_CARTAS;
    int idxComputador;
    do {
        idxComputador = rand() % TOTAL_CARTAS;
    } while (idxComputador == idxJogador); // evita cartas iguais

    Carta cartaJogador = baralho[idxJogador];
    Carta cartaComputador = baralho[idxComputador];

    printf("Sua carta:\n");
    mostrarCarta(cartaJogador);

    int escolha;
    printf("\nEscolha um atributo para competir (1 - Força, 2 - Velocidade, 3 - Inteligência): ");
    scanf("%d", &escolha);

    comparar(cartaJogador, cartaComputador, escolha);

    return 0;
}
