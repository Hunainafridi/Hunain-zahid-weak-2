#include <iostream>
#include <vector>
using namespace std;
void costSlab1(const vector<int>& slab) {
    cout << "Bill for Slab 1:\n";
    for (int i : slab) {
        cout << 10 * i << " ";
    }
    cout << endl;
}
void costSlab2(const vector<int>& slab) {
    cout << "Bill for Slab 2:\n";
    for (int i : slab) {
        cout << 10 * i << " ";
    }
    cout << endl;
}
void costSlab3(const vector<int>& slab) {
    cout << "Bill for Slab 3:\n";
    for (int i : slab) {
        cout << 10 * i << " ";
    }
    cout << endl;
}
int main() {
    vector<vector<int>> matrix = {{7, 6, 8}, {2, 4, 3}, {1, 8, 5}};
    string ID;
    cout << "Enter your ID: ";
    getline(cin, ID);
    cout << "Student's ID: " << ID << endl;
    cout << "Enter One of them:\n"
         << "1. Display Bill of Slab 1 and Slab 2\n"
         << "2. Display Bill of Slab 3\n"
         << "3. Exit\n";
    int choice;
    cout << "Enter your choice (1-3): ";
    cin >> choice;
    if (choice == 1) {
        costSlab1(matrix[0]);
        costSlab2(matrix[1]);
    } else if (choice == 2) {
        costSlab3(matrix[2]);
    } else {
        cout << endl;
    }
}
