
 /* This program encrypts and decrypts messages using the XOR Cipher
 Author: Abdallah Kareem Abdallah Ahmed
 ID : 20230228
 Date : 8/3/2024
 version 2.0 */

#include <iostream>
#include <string>
#include <iomanip>
#include <sstream>

using namespace std;

string encrypt(const string& message, const string& key) {
    string encrypted_hex;
    string cipher_text;
    for (char ch : message) {
        char temp = ch ^ key[(encrypted_hex.size() / 3) % key.size()];
        stringstream ss;
        ss << hex << setw(2) << setfill( 0 ) << static_cast<int>(temp);
        encrypted_hex += ss.str() + " "; // Add space between each character
        cipher_text += temp;
    }
    return cipher_text + " (Cipher) " + encrypted_hex + "(Hexadecimal)";
}

string decrypt(const string& message, const string& key) {
    string hex_to_text;
    for (size_t i = 0; i < message.size(); i += 3) { // Increase by 3 to skip spaces
        int temp;
        stringstream ss;
        ss << hex << message.substr(i, 2);
        ss >> temp;
        hex_to_text += static_cast<char>(temp);
    }

    string decrypted_result;
    for (char ch : hex_to_text) {
        char temp = ch ^ key[(decrypted_result.size() / 3) % key.size()];
        decrypted_result += temp;
    }
    return decrypted_result;
}

int main() {
    int choice;
    cout << "1. Encryption\n2. Decryption\nChoose(1,2): ";
    cin >> choice;

    if (choice == 1) {
        cout << "---Encryption---" << endl;
        string message, key;
        cout << "Enter message: ";
        cin.ignore();
        getline(cin, message);
        cout << "Enter key: ";
        getline(cin, key);
        string encrypted = encrypt(message, key);
        cout << "Encrypted Text: " << encrypted << endl;
    } else if (choice == 2) {
        cout << "---Decryption---" << endl;
        string message, key;
        cout << "Enter message (Hexadecimal): ";
        cin.ignore();
        getline(cin, message);
        cout << "Enter key: ";
        getline(cin, key);
        string decrypted = decrypt(message, key);
        cout << "Decrypted Text: " << decrypted << endl;
    } else {
        cout << "Invalid Choice" << endl;
    }

    return 0;
}
