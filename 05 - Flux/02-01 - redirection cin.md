# Redirection de cin, copier un fichier dans un autre

Modifier le programme en C++ de l'exercice 01-02 pour ajouter les fonctionnalités suivantes :

- Demander à l'utilisateur de saisir le nom d'un fichier source.
- Au lieu de saisir le texte, utiliser cin pour lire depuis le fichier source et ajouter (append) le texte dans le fichier de sortie. Si le fichier de sortie existe déjà, il ne doit pas être écrasé.


Ps. Le code utilisé pour l'écriture ne doit pas changer, comparé à l'exercice 01-02.   

~~~cpp 
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

bool lire_fichier(const string& nom_fichier){
    ifstream file_stream;

    file_stream.open(nom_fichier);

    if (!file_stream){
        return false;
    }

    string out;

    while(getline(nom_fichier, out)){
        cout << out << endl;
    }

    file_stream.close();

    return true;
}

bool ecrire_fichier(const string& nom_fichier){
    ofstream fichier_out;

    fichier_out.open(nom_fichier, ios::app);

    string line;
    while(getline(cin, line)){
        fichier_out << line << endl;
    }

    fichier_out.close()
}

int main(){

    string nom_fichier_out;

    do{
        cout << "Saisir un nom de fichier output : " << endl;
        getline(cin, nom_fichier_out);
    }
    while(nom_fichier_out.empty());
    lire_fichier(nom_fichier_out);

    string nom_fichier;
    do{
        cout << "Saisir un nom de fichier source : " << endl;
        getline(cin, nom_fichier);
    }
    while(nom_fichier.empty());

    auto cin_buf = cin.rdbut();

    ifstream fichier_in;
    fichier_in.open(nom_fichier.rdbuf());

    cin.rdbuf(fichier_in);

    ecrire_fichier(nom_fichier_out);

    cin.rdbuf(cin_buf);
    fichier_in.close();

    return EXIT_SUCCESS;
}

~~~

<details>
<summary>Solution</summary>

~~~cpp
#include <iostream>
#include <fstream>
#include <string>

bool lire_fichier(const std::string& nom_fichier){
    std::ifstream fichier_entree(nom_fichier);

    // Vérifier si l'ouverture du fichier a réussi
    if (!fichier_entree) {
        return false;
    }

    while (fichier_entree) {
        std::string strInput;
        std::getline(fichier_entree, strInput); // lire une ligne
        std::cout << strInput << "\n";
    }

    fichier_entree.close();

    return true;
}

bool ecrire_fichier(const std::string& nom_fichier) {

    // Ouvrir le fichier en mode append
    std::ofstream fichier_sortie(nom_fichier, std::ios::app);

    // Vérifier si l'ouverture du fichier a réussi
    if (!fichier_sortie) {
        std::cerr << "Erreur : Impossible d'ouvrir le fichier. \n";
        return false;
    }

    std::string texte;
    const std::string terminer = "#exit#";

    // Demander à l'utilisateur de saisir du texte
    std::cout << "Entrez le texte à enregistrer dans le fichier (Ctrl+D ou #exit# pour terminer la saisie) :\n";
    while (std::getline(std::cin, texte)) {
        if (texte == terminer) break;
        // Écrire le texte dans le fichier
        fichier_sortie << texte << std::endl;
    }

    // Fermer le fichier
    fichier_sortie.close();

    std::cout << "Le texte a été enregistré avec succès dans le fichier." << std::endl;

    return true;
}

int main() {
    std::string nom_fichier;

    // Demander à l'utilisateur le nom du fichier où enregistrer le texte
    std::cout << "Entrez le nom du fichier où enregistrer le texte : ";
    std::getline(std::cin, nom_fichier);

    lire_fichier(nom_fichier);

    std::string nom_fichier_src;
    // Demander à l'utilisateur le nom du fichier source
    std::cout << "Entrez le nom du fichier source : ";
    std::getline(std::cin, nom_fichier_src);

    std::ifstream fichier_entree(nom_fichier_src);

    // Vérifier si l'ouverture du fichier a réussi
    if (!fichier_entree) {
        std::cerr << "Erreur : Impossible d'ouvrir le fichier. \n";
        return EXIT_FAILURE;
    }

    auto cin_buf = std::cin.rdbuf();
    std::cin.rdbuf(fichier_entree.rdbuf());

    ecrire_fichier(nom_fichier);

    std::cin.rdbuf(cin_buf);
    fichier_entree.close();


    return EXIT_SUCCESS;
}

~~~



</details>
