#include <iostream>
#include <chrono>

using namespace std;

const int N = 100;

void main1(int arr[], int sort_arr[]) 
{
  for (int i = 0; i < N; i++)
  {
    int start = -99;
    int end = 99;
    arr[i] = rand() % (end - start + 1) + start;
    sort_arr[i] = arr[i];
  }
}
//buble sort
void buble(int bub[])
{
  auto start = chrono::high_resolution_clock::now();
  
  for (int i = 0; i < N - 1; i++) {
       bool flag = true;
      for (int j = 0; j < N - i - 1; j++) {
              if (bub[j] > bub[j + 1]) {
        flag = false;
        swap(bub[j], bub[j + 1]);
      }
    }
    if (flag) {
      break;
    }
  }
  auto end = chrono::high_resolution_clock::now();
  chrono::duration<double> duration = end - start;
  
  auto result = chrono::duration_cast<chrono::microseconds>(end - start);
  cout << "Отсортированный массив в порядке возрастания: " << endl;
  for (int i = 0; i < N; i++) {
    cout << "[" << bub[i] << "]" << " ";
  }
  cout << endl;
  cout << "Время затраченное на сортирову: " << result.count() << " микросекунд" << endl;
}
//shaker sort 
void shaker(int sh[]) 
{
  bool sort_or_not = true;
  int right = N - 1;
  int left = 1;
  auto start  = chrono::high_resolution_clock::now();
  do {
    bool sort_or_not = true;
    for (int i = left; i <= right; i++) 
    {
      if (sh[i - 1] > sh[i]) 
      {
        swap(sh[i - 1], sh[i]);
        sort_or_not = false;
      }
    }
    right--;
    for (int i = right; i >= left; i--) 
    {
      if (sh[i] < sh[i - 1]) 
      {
        swap(sh[i], sh[i - 1]);
        sort_or_not = false;
      }
    }
    left++;
  }
  while (sort_or_not == false);
  auto end = chrono::high_resolution_clock::now();
  chrono::duration<double> duration = end - start;
  
  auto result = chrono::duration_cast<chrono::microseconds>(end - start);
  cout << "Отсортированный массив в порядке возрастания: " << endl;
  for (int i = 0; i < N; i++) {
    cout << "[" << sh[i] << "]" << " ";
  }
  cout << endl;
  cout << "Время затраченное на сортирову: " << result.count() << " микросекунд" << endl;
}
//raschestka
int getNextGap(int gap)
{
  gap = (gap * 10) / 13;
  if (gap < 1)
    return 1;
  return gap;
}
void comb(int cm[]) 
{

  int gap = N;
  bool swapped = true;
  auto start = chrono::high_resolution_clock::now();
  while (gap != 1 || swapped == true)
  {
    gap = getNextGap(gap);
    swapped = false;
    for (int i = 0; i < N - gap; i++)
    {
      if (cm[i] > cm[i + gap])
      {
        swap(cm[i], cm[i + gap]);
        swapped = true;
      }
    }
  }
  auto end = chrono::high_resolution_clock::now();
  chrono::duration<double> duration = end - start;
  
  auto result = chrono::duration_cast<chrono::microseconds>(end - start);
  cout << "Отсортированный массив в порядке возрастания: " << endl;
  for (int i = 0; i < N; i++) {
    cout << "[" << cm[i] << "]" << " ";
  }
  cout << endl;
  cout << "Время затраченное на сортирову: " << result.count() << " микросекунд" << endl;
}
//vstavkami
void insert(int is[]) 
{

  int i, key, j;
  auto start = chrono::high_resolution_clock::now();
  for (i = 1; i < N; i++) 
  {
    key = is[i];
    j = i - 1;

    while (j >= 0 && is[j] > key) 
    {
      is[j + 1] = is[j];
      j = j - 1;
    }
    is[j + 1] = key;
  }
  auto end = chrono::high_resolution_clock::now();
  chrono::duration<double> duration = end - start;
  
  auto result = chrono::duration_cast<chrono::microseconds>(end - start);
  cout << "Отсортированный массив в порядке возрастания: " << endl;
  for (int i = 0; i < N; i++) {
    cout << "[" << is[i] << "]" << " ";
  }
  cout << endl;
  cout << "Время затраченное на сортирову: " << result.count() << " микросекунд" << endl;
}
//2 pynkt
void sort_m() 
{
  cout << "Варианты сортировок: " << endl;
  cout << "1.Bubble sort" << endl;
  cout << "2.Shaker sort" << endl;
  cout << "3.Comb sort" << endl;
  cout << "4.Insert sort" << endl;
}
void sort(int a[]) 
{
  sort_m();
  int b;
  cout << endl;
  cout << "Выберите номер сортировки: ";
  cin >> b;
  switch (b) 
  {
  case 1:
    buble(a);
    break;
  case 2:
    shaker(a);
    break;
  case 3:
    comb(a);
    break;
  case 4:
    insert(a);
    break;
  }
  cout << endl;
}
//3 pynkt
void findMinMax(int arr[]) {
  auto start = chrono::high_resolution_clock::now();
  int min = arr[0];
  int max = arr[0];
  for (int i = 1; i < N; i++) {
    if (arr[i] < min) {
      min = arr[i];
    }
    if (arr[i] > max) {
      max = arr[i];
    }
  }
  auto end = chrono::high_resolution_clock::now();
  auto result = chrono::duration_cast<chrono::microseconds>(end - start);
  cout << "Минимальный элемент в неотсортированном массиве: " << min << endl;
  cout << "Максимальный элемент в неотсортированном массиве: " << max << endl;
  cout << "Время затраченное на поиск в неотсортированном массиве: " << result.count() << " микросекунд" << endl;
}

void findMinMaxS(int arr[]) {
  auto start = chrono::high_resolution_clock::now();
  int min = arr[0];
  int max = arr[N - 1];
  auto end = chrono::high_resolution_clock::now();
  auto result = chrono::duration_cast<chrono::microseconds>(end - start);
  cout << "Минимальный элемент в отсортированном массиве: " << min << endl;
  cout << "Максимальный элемент в отсортированном массиве: " << max << endl;
  cout << "Время затраченное на поиск в отсортированном массиве: " << result.count() << " микросекунд" << endl;
}
//4 punkt
void srzn(int arr[])
{

  for (int i = 0; i < N; i++)
  {
    int start = -99;
    int end = 99;
    arr[i] = rand() % (end - start + 1) + start;

  }
  for (int i = 0; i < N; i++) 
  {
    cout << "[" << arr[i] << "]" << " ";

  }
  cout << endl;
  int b = (arr[0] + arr[N - 1]) / 2;
  cout << "Среднее значение максимального и минимального значения в неотсортированном массиве:" << endl;
  cout << b << endl;

  buble(arr);

  int a = (arr[0] + arr[N - 1]) / 2;
  cout << "Среднее значение максимального и минимального значения в отсортированном массиве:" << endl;
  cout << a << endl;

  int i = N - 1;
  while (arr[i] > a) 
  {
    i /= 2;
  }
  int k = 0;
  cout << "Индексы всех элементов, которые равны этому значению: " << endl;
  auto start = chrono::high_resolution_clock::now();
  for (int i = 0; i < N; i++) 
  {
    if (arr[i] == a) 
    {
      cout << i << " ";
      k++;
    }
  }

  auto end = chrono::high_resolution_clock::now();
  auto result = chrono::duration_cast<chrono::microseconds>(end - start);
  if (k == 0) cout << "Значения не найдены" << endl;
  cout << "Количество элементов: " << k << endl;
  cout << "Время поиска: " << result.count() << " микросекунд" << endl;
  cout << endl;
}
//5 pynkt
void kol_elemm(int arr[]) 
{
  buble(arr);
  int a;
  cout << "Введите число а:" << endl;
  cin >> a;
  int count = 0;
for (int i = 0; i < N; i++) 
  {
    if (arr[i] < a) 
    {
      count++;
    }
  }
  cout << "Количество элементов меньше " << a << ": " << count << endl; 
  cout << endl;
}
//6 pynkt
void kol_elemb(int arr[]) 
{
  buble(arr);
  int b;
  cout << "Введите число b:" << endl;
  cin >> b;
  int count = 0;
  for (int i = 0; i < N; ++i) 
  {
    if (arr[i] > b) 
    {
      ++count;
    }
  }
  cout << "Количество элементов больше " << b << ": " << count << endl;
  cout << endl;
}
//8 pynkt с божьей помощью 
void pomenka(int arr[]) 
{

  buble(arr);
  cout << "Введите индексы элементов для обмена: " << endl;
  int i1, i2;
  cin >> i1 >> i2;
  int temp = arr[i1];
  arr[i1] = arr[i2];
  arr[i2] = temp;
  auto start = chrono::high_resolution_clock::now();
  for (int i = 0; i < N; i++) 
  {
    temp = arr[i1];
    arr[i1] = arr[i2];
    arr[i2] = temp;
  }
  auto end = chrono::high_resolution_clock::now();
  auto result = chrono::duration_cast<chrono::microseconds>(end - start);
  cout << "Скорость обмена: " << 100000.0 / result.count() << " обменов в секунду" << endl;
  cout << "Отсортированный массив: " << endl;
  for (int i = 0; i < N; i++) 
  {
    cout << "[" << arr[i] << "]" << " ";
  }
  cout << endl;
  cout << endl;
}
int main() 
{
  setlocale(0, "");
  int choice;
  bool p = true;
  int arr[N], sort_arr[N];
  main1(arr, sort_arr);
  while (p)
  {
    cout << "Выберите номер задания:" << endl;
    cin >> choice;
    system("cls");
    switch (choice) 
    {
    case 0:
      cout << "Конец";
      return 0;
    case 1:
      main1(arr, sort_arr);
      for (int i = 0; i < N; i++)
      {
        cout << "[" << arr[i] << "]" << " ";
      }
      cout << endl;
      cout << endl;
      break;
    case 2:
      sort(sort_arr);
      break;
    case 3:
      findMinMaxS(arr);
      break;
    case 4:
      findMinMax(arr);
      break;
    case 5:
      srzn(arr);
      break;
    case 6:
      kol_elemm(arr);
      break;
    case 7:
      kol_elemb(arr);
      break;
    case 8:
      pomenka(arr);
      break;
    
    }
  }
  return 0;
}

