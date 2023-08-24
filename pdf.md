# daa1
Selection sort
import java.util.Scanner;
import java.util.Random;
public class SelectionsortComplexity {
static final int MAX = 200000;
static int[] a = new int[MAX];
public static void SelectionSortAlgorithm(int n) {
for (int i = 0; i < n - 1; i++) {
int minIndex = i;
for (int j = i + 1; j < n; j++) {
if (a[j] < a[minIndex]) {
minIndex = j;
}}
if (minIndex != i) {
int temp = a[i];
a[i] = a[minIndex];
a[minIndex] = temp;
}}}
public static void main(String[] args) {
Scanner input = new Scanner(System.in);
System.out.print("Enter Max array size: ");
int n = input.nextInt();
Random random = new Random();
System.out.println("Generating random array elements...");
for (int i = 0; i < n; i++) {
a[i] = random.nextInt();
}
System.out.println("Input Array:");
for (int i = 0; i < n; i++) {
System.out.print(a[i] + " ");
}
System.out.println();
long startTime = System.nanoTime();
System.out.println("\nSorting the array...");
SelectionSortAlgorithm(n);
System.out.println("Array Sorted!");

long stopTime = System.nanoTime();
long elapsedTime = stopTime - startTime;
System.out.println("\nSorted Array:");
for (int i = 0; i < n; i++) {
System.out.print(a[i] + " ");
}
System.out.println();
System.out.println("Time Complexity in ms for n=" + n + " is: " + (double) elapsedTime / 1000000);
}}
Quick sort
import java.util.Scanner;
import java.util.Random;
public class Quicksort {
static final int MAX = 200000;
static int[] a = new int[MAX];
public static void main(String[] args) {
Scanner input = new Scanner(System.in);
System.out.print("Enter Max array size: ");
int n = input.nextInt();
Random random = new Random();
System.out.println("Generating random array elements...");
for (int i = 0; i < n; i++) {
a[i] = random.nextInt(10000);
}
System.out.println("Input Array:");
for (int i = 0; i < n; i++)
System.out.print(a[i] + " ");
long startTime = System.nanoTime();
QuickSortAlgorithm(0, n - 1);
long stopTime = System.nanoTime();
long elapsedTime = stopTime - startTime;
System.out.println("\nSorted Array:");
for (int i = 0; i < n; i++)
System.out.print(a[i] + " ");
System.out.println();

System.out.println("Time Complexity in ms for n=" + n + " is: " + (double) elapsedTime / 1000000);
}
public static void QuickSortAlgorithm(int p, int r) {
int i, j, temp, pivot;
if (p < r) {
i = p;
j = r + 1;
pivot = a[p];
while (true) {
i++;
while (a[i] < pivot && i < r)
i++;
j--;
while (a[j] > pivot)
j--;
if (i < j) {
temp = a[i];
a[i] = a[j];
a[j] = temp;
} else
break;
}
a[p] = a[j];
a[j] = pivot;

QuickSortAlgorithm(p, j - 1);
QuickSortAlgorithm(j + 1, r);
}}}
Merge sort
import java.util.Random;
import java.util.Scanner;
public class Mergesort{
static final int MAX = 200000;
static int[] a = new int[MAX];
public static void main(String[] args) {
Scanner input = new Scanner(System.in);

System.out.print("Enter Max array size: ");
int n = input.nextInt();
Random random = new Random();
System.out.println("Enter the array elements: ");
for (int i = 0; i < n; i++)
{
a[i] = random.nextInt(100000);
System.out.print(a[i] + " ");
}
long startTime = System.nanoTime();
MergeSortAlgorithm(0, n - 1);
long stopTime = System.nanoTime();
long elapsedTime = stopTime - startTime;
System.out.println("Time Complexity (ms) for n = " + n + " is : " +
(double) elapsedTime / 1000000);
System.out.println("Sorted Array (Merge Sort):");
for (int i = 0; i < n; i++)
System.out.print(a[i] + " ");
input.close();
}
public static void MergeSortAlgorithm(int low, int high) {
int mid;
if (low < high) {
mid = (low + high) / 2;
MergeSortAlgorithm(low, mid);
MergeSortAlgorithm(mid + 1, high);
Merge(low, mid, high);
}
}
public static void Merge(int low, int mid, int high) {
int[] b = new int[MAX];
int i, h, j, k;
h = i = low;
j = mid + 1;
while ((h <= mid) && (j <= high))
if (a[h] < a[j])

b[i++] = a[h++];
else
b[i++] = a[j++];
if (h > mid)
for (k = j; k <= high; k++)
b[i++] = a[k];
else
for (k = h; k <= mid; k++)
b[i++] = a[k];
for (k = low; k <= high; k++)
a[k] = b[k];
}
}
Prims
import java.util.Scanner;
public class PrimsClass {
final static int MAX = 20;
static int n; // No. of vertices of G
static int cost[][]; // Cost matrix
static Scanner scan = new Scanner(System.in);
public static void main(String[] args) {
ReadMatrix();
Prims();
}
static void ReadMatrix() {
int i, j;
cost = new int[MAX][MAX];
System.out.println("\n Enter the number of nodes:");
n = scan.nextInt();
System.out.println("\n Enter the cost matrix:\n");
for (i = 1; i <= n; i++)
for (j = 1; j <= n; j++) {
cost[i][j] = scan.nextInt();
if (cost[i][j] == 0)
cost[i][j] = 999;
}}

static void Prims() {
int visited[] = new int[10];
int ne = 1, i, j, min, a = 0, b = 0, u = 0, v = 0;
int mincost = 0;
visited[1] = 1;
while (ne < n) {
for (i = 1, min = 999; i <= n; i++)
for (j = 1; j <= n; j++)
if (cost[i][j] < min)
if (visited[i] != 0) {
min = cost[i][j];
a = u = i;
b = v = j;
}
if (visited[u] == 0 || visited[v] == 0) {
System.out.println("Edge" + ne++ + ":(" + a + "," + b + ")" + "cost:" + min);
mincost += min;
visited[b] = 1;
}
cost[a][b] = cost[b][a] = 999;
}
System.out.println("\n Minimun cost" + mincost);
}
}
Kruskals
import java.util.Scanner;
public class kruskal {
static int parent[];
public static void main(String[] args) {
final int MAX = 20;
int n; // No. of vertices of G
int cost[][]; // Cost matrix
int a = 0, b = 0, u = 0, v = 0, ne = 1, min, mincost = 0;
parent = new int[MAX]; cost = new int[MAX][MAX];
Scanner scan = new Scanner(System.in);
System.out.println("Enter the no. of vertices");

n = scan.nextInt();
System.out.println("Enter the cost adjacency matrix");
for (int i = 1; i <= n; i++) {
for (int j = 1; j <= n; j++) {
cost[i][j] = scan.nextInt();
if (cost[i][j] == 0)
cost[i][j] = 999;
}
}
System.out.println("The edges of Minimum Cost Spanning Tree are");
while (ne < n) {
min= 999;
for (int i =1; i <= n; i++) {
for (int j = 1; j <= n; j++) {
if (cost[i][j] < min) {
min = cost[i][j];
a = u = i; b = v = j; } } }
u = find(u); v = find(v);
if (u != v) {
ne++;
System.out.println("edge " + a + "-->" + b + " =" + min);
mincost += min;
uni(a, v); }
cost[a][b] = cost[b][a] = 999; }
System.out.println("Minimum cost :" + mincost);
}
static int find(int i)
{
while (parent[i] != 0)
i = parent[i];
return i;
}
static void uni(int i, int j)
{
parent[j] = i;
}}

Dijkstras
import java.util.*;
public class dijkstras{
final static int MAX = 20;
final static int infinity = 9999;
static int n; // No. of vertices of G
static int a[][]; // Cost matrix
static Scanner scan = new Scanner(System.in);
public static void main(String[] args) {
ReadMatrix();
int s = 0; // starting vertex
System.out.println("Enter starting vertex: ");
s = scan.nextInt();
Dijkstras(s); // find shortest path
}
static void ReadMatrix() {
a = new int[MAX][MAX];
System.out.println("Enter the number of vertices:");
n = scan.nextInt();
System.out.println("Enter the cost adjacency matrix:");
for (int i = 1; i <= n; i++)
for (int j = 1; j <= n; j++)
a[i][j] = scan.nextInt();
}
static void Dijkstras(int s) {
int S[] = new int[MAX];
int d[] = new int[MAX];
int u, v;
int i;
for (i = 1; i <= n; i++) {
S[i] = 0;
d[i] = a[s][i];
}
S[s] = 1;
d[s] = 1;
i = 2;

while (i <= n) {
u = Extract_Min(S, d);
S[u] = 1;
i++;
for (v = 1; v <= n; v++) {
if (((d[u] + a[u][v] < d[v]) && (S[v] == 0)))
d[v] = d[u] + a[u][v];
}
}
for (i = 1; i <= n; i++)
if (i != s)
System.out.println(i + ":" + d[i]);
}
static int Extract_Min(int S[], int d[]) {
int i, j = 1, min;
min = infinity;
for (i = 1; i <= n; i++) {
if ((d[i] < min) && (S[i] == 0)) {
min = d[i];
j = i;
}
}
return (j);
}
}
