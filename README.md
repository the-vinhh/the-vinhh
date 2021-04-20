#include <iostream>
#include <string>
#include <iomanip>
#include <ctime>
#include <fstream>
using namespace std;

bool Input(int*, int, string);
bool Input(double*, int, string);
//void swap(int&, int&);
//void swap(double&, double&);
int Partition(int*, int, int);
void QuickSort(int*, int, int);
void Heapify(int*, int, int);
void HeapSort(int*, int);
int Partition(double*, int, int);
void QuickSort(double*, int, int);
void Heapify(double*, int, int);
void HeapSort(double*, int);
void TestSort(string[], int);

void InterchangeSort(int*, int);


int main()
{
    string f_name[10] = { "1.inp","2.inp" ,"3.inp" ,"4.inp" ,"5.inp" ,"6.inp" ,"7.inp" ,"8.inp" ,"9.inp" ,"10.inp" };
    int n = 100000;
    TestSort(f_name, n);

	return 0;
}

bool Input(int* a, int n, string filename)
{
    ifstream input;
    input.open(filename, ios::in);

    if (!input.is_open())
    {
        cout << "Khong the mo file.";
        return false;
    }

    string line = "";
    int i = 0;

    while (!input.eof() && i < n)
    {
        input >> line;
        if (line != "")
            a[i] = stoi(line);
        i++;
    }

    input.close();

    return true;
}

bool Input(double* a, int n, string filename)
{
    ifstream input;
    input.open(filename, ios::in);

    if (!input.is_open())
    {
        cout << "Khong the mo file.";
        return false;
    }

    string line = "";
    int i = 0;

    while (!input.eof() && i < n)
    {
        input >> line;
        if (line != "")
            a[i] = stof(line);
        i++;
    }

    input.close();

    return true;
}

//void swap(int& a, int& b)
//{
//    int t = a;
//    a = b;
//    b = t;
//}
//
//void swap(double& a, double& b)
//{
//    double t = a;
//    a = b;
//    b = t;
//}

//====================================================

int Partition(int* a, int low, int high)
{
    int pivot = a[high];
    int i = (low - 1);

    for (int j = low; j < high; j++)
    {
        if (a[j] < pivot)
        {
            i++;
            swap(a[i], a[j]);
        }
    }
    swap(a[i + 1], a[high]);

    return (i + 1);
}

void QuickSort(int* a, int low, int high)
{
    if (low < high)
    {
        int pi = Partition(a, low, high);

        QuickSort(a, low, pi - 1);
        QuickSort(a, pi + 1, high);
    }
}

void Heapify(int* a, int n, int i)
{
    int largest = i;
    int l = 2 * i + 1;
    int r = 2 * i + 2;

    if (l < n && a[l] > a[largest])
        largest = l;

    if (r < n && a[r] > a[largest])
        largest = r;

    if (largest != i) {
        swap(a[i], a[largest]);

        Heapify(a, n, largest);
    }
}

void HeapSort(int* a, int n)
{
    for (int i = n / 2 - 1; i >= 0; i--)
        Heapify(a, n, i);

    for (int i = n - 1; i > 0; i--)
    {
        swap(a[0], a[i]);

        Heapify(a, i, 0);
    }
}

//====================================================

int Partition(double* a, int low, int high)
{
    double pivot = a[high];
    int i = (low - 1);

    for (int j = low; j < high; j++)
    {
        if (a[j] < pivot)
        {
            i++;
            swap(a[i], a[j]);
        }
    }
    swap(a[i + 1], a[high]);

    return (i + 1);
}

void QuickSort(double* a, int low, int high)
{
    if (low < high)
    {
        int pi = Partition(a, low, high);

        QuickSort(a, low, pi - 1);
        QuickSort(a, pi + 1, high);
    }
}

void Heapify(double* a, int n, int i)
{
    int largest = i;
    int l = 2 * i + 1;
    int r = 2 * i + 2;

    if (l < n && a[l] > a[largest])
        largest = l;

    if (r < n && a[r] > a[largest])
        largest = r;

    if (largest != i) {
        swap(a[i], a[largest]);

        Heapify(a, n, largest);
    }
}

void HeapSort(double* a, int n)
{
    for (int i = n / 2 - 1; i >= 0; i--)
        Heapify(a, n, i);

    for (int i = n - 1; i > 0; i--)
    {
        swap(a[0], a[i]);

        Heapify(a, i, 0);
    }
}

void TestSort(string f_name[], int n)
{
    clock_t t;
    int* int_1 = new int[n];
    if (int_1 == NULL)
        return;
    int* int_2 = new int[n];
    if (int_2 == NULL)
        return;

    for (size_t i = 0; i < 5; i++)
    {
        cout << "Load file...\n";
        if (Input(int_1, n, f_name[i]))
        {
            int_2 = int_1;
            cout << "Load thanh cong file " << f_name[i] << "\n";
        }
        else
            return;
 
        cout << "Sorting...";
        
        //t = clock();
        //InterchangeSort(int_1, n);
        //t = clock() - t;
        //cout << "\nThoi gian thuc thi cua interchange sort: " << t << "s";
        //cout << endl;

        t = clock();
        QuickSort(int_1, 0, n - 1);
        t = clock() - t;
        cout << "\nThoi gian thuc thi cua quick sort: " << t << " s";

        t = clock();
        HeapSort(int_2, n);
        t = clock() - t;
        cout << "\nThoi gian thuc thi cua heap sort: " << t << "ms";
        cout << endl;
    }

    delete[]int_1, int_2;
    int_1 = int_2 = NULL;

    double* double_1 = new double[n];
    if (double_1 == NULL)
        return;
    double* double_2 = new double[n];
    if (double_2 == NULL)
        return;
    double_2 = double_1;

    for (int i = 5; i < 10; i++)
    {
        cout << "Load file...\n";
        if (Input(double_1, n, f_name[i]))
        {
            double_2 = double_1;
            cout << "Load thanh cong file " << f_name[i] << "\n";
        }
        else
            return;

        cout << "Sorting...";

        //t = clock();
        //QuickSort(float_1, 0, n - 1);
        //t = clock() - t;
        //cout << "\nThoi gian thuc thi cua quick sort: " << t << "s";

        t = clock();
        HeapSort(double_2, n);
        t = clock() - t;
        cout << "\nThoi gian thuc thi cua heap sort: " << t << "ms";
        cout << endl;
    }

    delete[]double_1, double_2;
    double_1 = double_2 = NULL;
}

void InterchangeSort(int* a, int n)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            if (a[i] > a[j])
            {
                swap(a[i], a[j]);
            }
        }
    }
}
