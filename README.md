#include <iostream>
using namespace std;
void createShiftTable(string pattern, int shiftTable[]) {
    int m = pattern.length();
    
    for (int i = 0; i < 256; i++) {
        shiftTable[i] = m;
    }
    
    for (int i = 0; i < m - 1; i++) {
        shiftTable[(unsigned char)pattern[i]] = m - 1 - i;
    }
}
int horspoolSearch(string text, string pattern) {
    int n = text.length();
    int m = pattern.length();
    if (m > n) return -1;
    
    int shiftTable[256];
    createShiftTable(pattern, shiftTable);
    
    int i = m - 1;
    while (i < n) {
        int j = 0;
        while (j < m && pattern[m - 1 - j] == text[i - j]) {
            j++;
        }
        if (j == m) {
            return i - m + 1;
        }
        
        i += shiftTable[(unsigned char)text[i]];
    }
    return -1;
}
int main() {
    string text = "THIS IS A SIMPLE EXAMPLE";
    string pattern = "EXAMPLE";
    
    int result = horspoolSearch(text, pattern);
    if (result != -1) {
        cout << "Pattern found at index " << result << endl;
    } else {
        cout << "Pattern not found" << endl;
    }
    
    return 0;
