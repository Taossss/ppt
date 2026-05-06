<script setup>
const props = defineProps({
  id: {
    type: String,
    required: true,
  },
})

const codes = {
  fib1: `main()
{
  int i, a = 1, b = 1, c;
  print(a, b);
  for (i = 1; i <= 10; i++) {
    c = a + b;
    print(c);
    a = b;
    b = c;
  }
}`,
  fib2: `main()
{
  int i, a = 1, b = 1, c;
  print(a, b);
  for (i = 1; i <= 4; i++) {
    c = a + b;
    a = b + c;
    b = c + a;
    print(a, b, c);
  }
}`,
  fib3: `main()
{
  int i, a = 1, b = 1;
  print(a, b);
  for (i = 1; i <= 5; i++) {
    a = a + b;
    b = a + b;
    print(a, b);
  }
}`,
  gcd: `main()
{
  int a, b, c;
  input(a, b);
  if (b == 0) {
    print("data error");
    return;
  }
  c = a % b;
  while (c != 0) {
    a = b;
    b = c;
    c = a % b;
  }
  print(b);
}`,
  peach: `main()
{
  int i, s;
  s = 1;
  for (i = 9; i >= 1; i = i - 1)
    s = (s + 1) * 2;
  print(s);
}`,
  pascal: `main()
{
  int n, i, j, a[100];
  input(n);
  print("1"); print("换行符");
  a[1] = a[2] = 1;
  for (i = 3; i <= n; i = i + 1) {
    a[1] = a[i] = 1;
    for (j = i - 1; j > 1; j--)
      a[j] = a[j] + a[j - 1];
    for (j = 1; j <= i; j = j + 1)
      print(a[j]);
    print("换行符");
  }
}`,
  desert: `main()
{
  int dis, k, oil;
  dis = 500;
  k = 1;
  oil = 500;
  do {
    print(k, 1000 - dis, oil);
    k = k + 1;
    dis = dis + 500 / (2 * k - 1);
    oil = 500 * k;
  } while (dis < 1000);
  oil = 500 * (k - 1) + (1000 - dis) * (2 * k - 1);
  print(k, 0, oil);
}`,
  system: `for (i = 0; i < n; i++)
  x[i] = 初始近似根;
do {
  k = k + 1;
  for (i = 0; i < n; i++) y[i] = x[i];
  for (i = 0; i < n; i++) x[i] = gi(X);
  for (i = 0; i < n; i++)
    c = c + fabs(y[i] - x[i]);
} while (c > w && k < maxn);

for (i = 0; i < n; i++)
  print(i, "变量的近似根是", x[i]);`,
  newton: `main()
{
  float a, b, c, d, fx;
  print("输入系数 a,b,c,d:");
  input(a, b, c, d);
  fx = f(a, b, c, d);
  printf("方程的根为：", fx);
}

float f(a, b, c, d)
  float a, b, c, d;
{
  float x1 = 1, x0, f0, f1;
  do {
    x0 = x1;
    f0 = ((a * x0 + b) * x0 + c) * x0 + d;
    f1 = (3 * a * x0 + 2 * b) * x0 + c;
    x1 = x0 - f0 / f1;
  } while (fabs(x1 - x0) >= 1e-4);
  return x1;
}`,
  bisection: `main()
{
  float x, x1 = 0, x2 = 2, f1, f2, f;
  input(a, b);
  f1 = x1*x1*x1/2 + 2*x1*x1 - 8;
  f2 = x2*x2*x2/2 + 2*x2*x2 - 8;
  if (f1 * f2 > 0) {
    printf("No root");
    return;
  }
  do {
    x = (x1 + x2) / 2;
    f = x*x*x/2 + 2*x*x - 8;
    if (f == 0) break;
    if (f1 * f > 0.0) {
      x1 = x; f1 = f;
    } else {
      x2 = x; f2 = f;
    }
  } while (fabs(f) >= 1e-4);
  print("root=", x);
}`,
}
</script>

<template>
  <pre class="code-window">{{ codes[props.id] }}</pre>
</template>
