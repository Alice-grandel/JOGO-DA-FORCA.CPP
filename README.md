# 🎯 Jogo da Forca em c++

Um jogo da forca simples feito em C++ rodando no terminal. O objetivo é adivinhar a palavra secreta, letra por letra, com no máximo 6 erros.
💻 Tecnologias usadas



## 🧬 Tecnologias usadas

- Linguagem: **c++**
- Conceitos utilizados:

   - `std::vector`
  
   - `std::string`
  
   - `Laços de repetição (for, while)`
  
   - `Funções`

   - `Condicionais (if, else)`
  
   - `Leitura de dados com std::cin`
  
   - `Escrita com std::cout`
  
   - `Comparação de caracteres`
  
   - `Lógica básica de jogo`
  
   - `Manipulação de caracteres com tolower()`


# CODIGO:
```
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

void mostrarPalavra(const string& palavra, const vector<bool>& letrasDescobertas) {
    for (size_t i = 0; i < palavra.size(); ++i) {
        if (letrasDescobertas[i])
            cout << palavra[i] << " ";
        else
            cout << "_ ";
    }
    cout << endl;
}

bool letraJaTentada(const vector<char>& letrasTentadas, char letra) {
    return find(letrasTentadas.begin(), letrasTentadas.end(), letra) != letrasTentadas.end();
}

int main() {
    string palavra = "programacao";
    vector<bool> letrasDescobertas(palavra.size(), false);
    vector<char> letrasTentadas;

    int chances = 6;
    bool ganhou = false;

    cout << "=== Jogo da Forca ===" << endl;

    while (chances > 0 && !ganhou) {
        mostrarPalavra(palavra, letrasDescobertas);

        cout << "Chances restantes: " << chances << endl;
        cout << "Digite uma letra: ";
        char letra;
        cin >> letra;

        // Converte para minúsculo
        letra = tolower(letra);

        if (letraJaTentada(letrasTentadas, letra)) {
            cout << "Você já tentou essa letra. Tente outra." << endl;
            continue;
        }

        letrasTentadas.push_back(letra);

        bool acertou = false;
        for (size_t i = 0; i < palavra.size(); ++i) {
            if (palavra[i] == letra) {
                letrasDescobertas[i] = true;
                acertou = true;
            }
        }

        if (!acertou) {
            chances--;
            cout << "Letra incorreta!" << endl;
        } else {
            cout << "Boa! Letra correta." << endl;
        }

        // Verifica se ganhou
        ganhou = true;
        for (bool descoberto : letrasDescobertas) {
            if (!descoberto) {
                ganhou = false;
                break;
            }
        }
    }

    if (ganhou)
        cout << "Parabéns! Você ganhou! A palavra era: " << palavra << endl;
    else
        cout << "Fim de jogo! Você perdeu! A palavra era: " << palavra << endl;

    return 0;
}
```
