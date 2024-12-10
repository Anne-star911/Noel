#include <iostream>
#include <windows.h>
#include <cstdlib>
#include <ctime>
#include <thread>

using namespace std;

// Hàm đặt màu cho text
void setColor(int color) {
    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), color);
}

// Hàm vẽ cây thông
void drawTree(int height) {
    for (int i = 0; i < height; i++) {
        // In khoảng trắng
        for (int j = 0; j < height - i - 1; j++) {
            cout << " ";
        }
        // In ngôi sao với màu sắc ngẫu nhiên
        for (int j = 0; j < 2 * i + 1; j++) {
            int color = rand() % 6 + 10; // Lựa chọn màu từ 10 đến 15
            setColor(color);
            cout << "*";
        }
        cout << endl;
    }
    // Thân cây
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < height - 2; j++) {
            cout << " ";
        }
        setColor(6); // Màu vàng
        cout << "||" << endl;
    }
}

// Hiệu ứng tuyết rơi
void snowEffect(int height) {
    while (true) {
        setColor(15); // Màu trắng
        for (int i = 0; i < height; i++) {
            cout << " ";
        }
        cout << "*" << endl;
        this_thread::sleep_for(chrono::milliseconds(200));
    }
}

int main() {
    srand(time(0));

    // Chiều cao cây thông
    int height = 10;

    // Vẽ cây thông
    drawTree(height);

    // Hiệu ứng tuyết rơi
    thread snow(snowEffect, height);
    snow.detach();

    // Đợi người dùng nhấn phím để thoát
    cin.get();
    return 0;
}
