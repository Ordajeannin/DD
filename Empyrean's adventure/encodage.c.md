
#include <stdio.h>
#include <ctype.h>

void encryptCesar(FILE *inputFile, FILE *outputFile, int shift) {
    char ch;

    while ((ch = fgetc(inputFile)) != EOF) {
        if (isalpha(ch)) {
            char base = (islower(ch)) ? 'a' : 'A';
            ch = (ch - base + shift) % 26 + base;
        }
        fputc(ch, outputFile);
    }
}

int main(int ac, char **av) {
    FILE *inputFile, *outputFile;
    int shift;

	if (ac < 3)
	{
		printf("usage : ./a.out infile outfile\n");
		return 0;
	}
    // Ouverture du fichier en lecture
    inputFile = fopen(av[1], "r");
    if (inputFile == NULL) {
        perror("Erreur lors de l'ouverture du fichier en lecture");
        return 1;
    }

    // Ouverture du fichier en écriture
    outputFile = fopen(av[2], "w");
    if (outputFile == NULL) {
        perror("Erreur lors de l'ouverture du fichier en écriture");
        fclose(inputFile);
        return 1;
    }

    // Demande du décalage à l'utilisateur
    printf("Entrez le décalage pour le chiffrement de César : ");
    scanf("%d", &shift);

    // Appel de la fonction d'encryption
    encryptCesar(inputFile, outputFile, shift);

    // Fermeture des fichiers
    fclose(inputFile);
    fclose(outputFile);

    printf("Chiffrement de César terminé avec succès.\n");

    return 0;
}
