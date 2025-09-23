# 1.
- Dữ liệu:

| Obj | t1 (nomial) | t2 (ordinal) | t3 (numeric) | t4 (nomial) | t5 (ordinal) |
|-----|-------------|--------------|--------------|--------------| -------------|
| S1  | A           | Cao          | 8.5          | X            |    1         |
| S2  | B           | Trung bình   | 7.0          | Z            |    2        |
| S3  | A           | Thấp         | 9.0          | Y            |    1         |
| S4  | B           | Cao          | 8.0          | X            |    2         |


- Mục tiêu: Tính ma trận bất tương đồng cho từng thuộc tính.

## Ma trận bất tương đồng cho thuộc tính Danh nghĩa (Nominal attributes)

|     | t1 (nomial) | t4 (nomial) |
|-----|-------------|--------------|
| S1  | 0           | 0            |
| S2  | 1           | 1            |
| S3  | 0           | 1            |
| S4  | 1           | 0            |

- Công thức: $d(i, j) = \frac{p - m}{p}$ 
  - $p$: số thuộc tính
  - $m$: số thuộc tính giống nhau
- Ta thấy: $p = 2$ (t1, t4)
- Tính toán:
$$
d(1, 2) = \frac{2 - 0}{2} = 1.0 \\[2em]
d(1, 3) = \frac{2 - 1}{2} = 0.5 \\[2em]
d(1, 4) = \frac{2 - 1}{2} = 0.5 \\[2em]
d(2, 3) = \frac{2 - 0}{2} = 1.0 \\[2em]
d(2, 4) = \frac{2 - 1}{2} = 0.5 \\[2em]
d(3, 4) = \frac{2 - 0}{2} = 1.0
$$

- Ma trận bất tương đồng:
$$
\begin{bmatrix}
0 & 1.0 & 0.5 & 0.5 \\
1.0 & 0 & 1.0 & 0.5 \\
0.5 & 1.0 & 0 & 1.0 \\
0.5 & 0.5 & 1.0 & 0 \\
\end{bmatrix}
$$

## Ma trận bất tương đồng cho thuộc tính Thứ bậc (Ordinal attributes)

|     | t2 (ordinal) | t5 (ordinal) |
|-----|--------------|--------------|
| S1  | Cao (3)      | 1            |
| S2  | Trung bình(2)| 2            |
| S3  | Thấp (1)     | 1            |
| S4  | Cao (3)      | 2            |

- Công thức:
    - $z = \frac{r - 1}{M_f - 1}$
        - $r$: hạng của giá trị
        - $M_f$: số mức độ (số hạng)

- Ánh xạ:
  - t2: Thấp=1, Trung bình=2, Cao=3 → $M_f = 3$
  - t5: 1, 2 → $M_f = 2$
- Chuẩn hóa cho t2:
  - Thấp (r=1): $z = \frac{1-1}{3-1} = \frac{0}{2} = 0.0$
  - Trung bình (r=2): $z = \frac{2-1}{3-1} = \frac{1}{2} = 0.5$
  - Cao (r=3): $z = \frac{3-1}{3-1} = \frac{2}{2} = 1.0$

- Chuẩn hóa cho t5:
  - 1 (r=1): $z = \frac{1-1}{2-1} = \frac{0}{1} = 0.0$
  - 2 (r=2): $z = \frac{2-1}{2-1} = \frac{1}{1} = 1.0$
- Ta có giá trị chuẩn hóa:
  
|     | t2 (z) | t5 (z) |
|-----|--------|--------|
| S1  | 1.0    | 0.0    |
| S2  | 0.5    | 1.0    |
| S3  | 0.0    | 0.0    |
| S4  | 1.0    | 1.0    |

- Ta có công thức tính độ tương đồng:
    - Theo khoảng cách Minkowski:
        - $d(i, j) = \left( \sum_{k=1}^{h} |x_{ik} - x_{jk}|^h \right)^{\frac{1}{h}}$
            - Trong đó:
              - $p$: số thuộc tính
              - $h$: tham số (r=1: Manhattan, r=2: Euclidean)
              - $x_{ik}$: giá trị chuẩn hóa của đối tượng i tại thuộc tính k
              - $x_{jk}$: giá trị chuẩn hóa của đối tượng j tại thuộc tính k
            - Khi $r=\infty$: Supremum distance, thì:
              - $d(i, j) = \max_{k} |x_{ik} - x_{jk}|$
            - Khi có trọng số $w_k$ cho thuộc tính k:
              - $d(i, j) = \left( \sum_{k=1}^{p} w_k |x_{ik} - x_{jk}|^h \right)^{\frac{1}{h}}$
- Ở đây ta dùng khoảng cách Euclidean (h=2):
    - $d(i, j) = \left( \sum_{k=1}^{p} |x_{ik} - x_{jk}|^2 \right)^{\frac{1}{2}}$
- Tính toán:
$$d(1, 2) = \sqrt{(1.0 - 0.5)^2 + (0.0 - 1.0)^2} = \sqrt{0.25 + 1.0} = \sqrt{1.25} \approx 1.118 \\[2em]
d(1, 3) = \sqrt{(1.0 - 0.0)^2 + (0.0 - 0.0)^2} = \sqrt{1.0 + 0.0} = \sqrt{1.0} = 1.0 \\[2em]
d(1, 4) = \sqrt{(1.0 - 1.0)^2 + (0.0 - 1.0)^2} = \sqrt{0.0 + 1.0} = \sqrt{1.0} = 1.0 \\[2em]
d(2, 3) = \sqrt{(0.5 - 0.0)^2 + (1.0 - 0.0)^2} = \sqrt{0.25 + 1.0} = \sqrt{1.25} \approx 1.118 \\[2em]
d(2, 4) = \sqrt{(0.5 - 1.0)^2 + (1.0 - 1.0)^2} = \sqrt{0.25 + 0.0} = \sqrt{0.25} = 0.5 \\[2em]
d(3, 4) = \sqrt{(0.0 - 1.0)^2 + (0.0 - 1.0)^2} = \sqrt{1.0 + 1.0} = \sqrt{2.0} \approx 1.414
$$ 

- Ma trận bất tương đồng:
$$
\begin{bmatrix}
0 & 1.118 & 1.0 & 1.0 \\
1.118 & 0 & 1.118 & 0.5 \\
1.0 & 1.118 & 0 & 1.414 \\
1.0 & 0.5 & 1.414 & 0 \\
\end{bmatrix}
$$

## Ma trận bất tương đồng cho thuộc tính Số (Numeric attributes)
|     | t3 (numeric) |
|-----|--------------|
| S1  | 8.5          |
| S2  | 7.0          |
| S3  | 9.0          |
| S4  | 8.0          |  

- Công thức:
    - Theo khoảng cách Minkowski:
        - $d(i, j) = \left( \sum_{k=1}^{h} |x_{ik} - x_{jk}|^h \right)^{\frac{1}{h}}$
            - Trong đó:
              - $p$: số thuộc tính
              - $h$: tham số (r=1: Manhattan, r=2: Euclidean)
              - $x_{ik}$: giá trị chuẩn hóa của đối tượng i tại thuộc tính k
              - $x_{jk}$: giá trị chuẩn hóa của đối tượng j tại thuộc tính k
            - Khi $r=\infty$: Supremum distance, thì:
              - $d(i, j) = \max_{k} |x_{ik} - x_{jk}|$
            - Khi có trọng số $w_k$ cho thuộc tính k:
              - $d(i, j) = \left( \sum_{k=1}^{p} w_k |x_{ik} - x_{jk}|^h \right)^{\frac{1}{h}}$

- Chuẩn hóa:
  - Giá trị: 8.5, 7.0, 9.0, 8.0 → $\min = 7.0$, $\max = 9.0$, khoảng = 2.0
  - Chuẩn hóa: $z = \frac{x - \min}{\max - \min} = \frac{x - 7.0}{2.0}$
  
- Giá trị chuẩn hóa:
  
|     | t3 (z) |
|-----|--------|
| S1  | 0.75   |
| S2  | 0.0    |
| S3  | 1.0    |
| S4  | 0.5    |

- Ở đây ta dùng khoảng cách Euclidean (h=2):
    - $d(i, j) = \left( \sum_{k=1}^{p} |x_{ik} - x_{jk}|^2 \right)^{\frac{1}{2}}$
  
- Tính toán:
$$d(1, 2) = \sqrt{(0.75 - 0.0)^2} = \sqrt{0.5625} = 0.75 \\[2em]
d(1, 3) = \sqrt{(0.75 - 1.0)^2} = \sqrt{0.0625} = 0.25 \\[2em]
d(1, 4) = \sqrt{(0.75 - 0.5)^2} = \sqrt{0.0625} = 0.25 \\[2em]
d(2, 3) = \sqrt{(0.0 - 1.0)^2} = \sqrt{1.0} = 1.0 \\[2em]
d(2, 4) = \sqrt{(0.0 - 0.5)^2} = \sqrt{0.25} = 0.5 \\[2em]
d(3, 4) = \sqrt{(1.0 - 0.5)^2} = \sqrt{0.25} = 0.5
$$

- Ma trận bất tương đồng:
$$
\begin{bmatrix}
0 & 0.75 & 0.25 & 0.25 \\
0.75 & 0 & 1.0 & 0.5 \\
0.25 & 1.0 & 0 & 0.5 \\
0.25 & 0.5 & 0.5 & 0 \\
\end{bmatrix}
$$

## Ma trận bất tương đồng cho hỗn hợp (Mixed attributes)

- Công thức:
    - $d(i, j) = \frac{\sum_{k=1}^{p} w_k d_{ijk}}{\sum_{k=1}^{p} w_k}$
        - $p$: số thuộc tính
        - $w_k$: trọng số của thuộc tính k (mặc định = 1)
        - $d_{ijk}$: độ bất tương đồng giữa đối tượng i và j tại thuộc tính k
            - Với thuộc tính danh nghĩa (nominal):
                - $d_{ijk} = 0$ nếu giống nhau, $d_{ijk} = 1$ nếu khác nhau
            - Với thuộc tính thứ bậc (ordinal):
                - Chuẩn hóa về [0,1]: $z = \frac{r - 1}{M_f - 1}$
                - $d_{ijk} = |z_i - z_j|$
            - Với thuộc tính số (numeric):
                - Chuẩn hóa về [0,1]: $z = \frac{x - \min}{\max - \min}$
                - $d_{ijk} = |z_i - z_j|$
                - Hoặc dùng khoảng cách Euclidean, Manhattan,...

### Ví dụ ma trận bất tương đồng hỗn hợp cho dữ liệu trên

- Tính $d_{ijk}$ cho từng thuộc tính:
  - t1 (nomial): $d_{ijk}$ theo danh nghĩa
  - t2 (ordinal): $d_{ijk}$ theo thứ bậc
  - t3 (numeric): $d_{ijk}$ theo số
  - t4 (nomial): $d_{ijk}$ theo danh nghĩa
  - t5 (ordinal): $d_{ijk}$ theo thứ bậc 
- Trọng số: $w_k = 1$ cho tất cả thuộc tính
- Số thuộc tính: $p = 5$
- Tính toán ma trận bất tương đồng hỗn hợp:
$$d(i, j) = \frac{\sum_{k=1}^{5} d_{ijk}}{5}$$
- Tính toán:
$$d(1, 2) = \frac{1 + 0.5 + 0.75 + 1 + 1.0}{5} = \frac{4.25}{5} = 0.85 \\[2em]
d(1, 3) = \frac{0 + 1.0 + 0.25 + 1 + 0.0}{5} = \frac{2.25}{5} = 0.45 \\[2em]
d(1, 4) = \frac{1 + 0.0 + 0.25 + 0 + 1.0}{5} = \frac{2.25}{5} = 0.45 \\[2em]
d(2, 3) = \frac{1 + 1.0 + 1.0 + 1 + 1.0}{5} = \frac{5.0}{5} = 1.0 \\[2em]
d(2, 4) = \frac{0 + 0.5 + 0.5 + 1 + 0.0}{5} = \frac{2.0}{5} = 0.4 \\[2em]
d(3, 4) = \frac{1 + 1.0 + 0.5 + 1 + 1.0}{5} = \frac{4.5}{5} = 0.9
$$
- Ma trận bất tương đồng hỗn hợp:
$$
\begin{bmatrix}
0 & 0.85 & 0.45 & 0.45 \\
0.85 & 0 & 1.0 & 0.4 \\
0.45 & 1.0 & 0 & 0.9 \\
0.45 & 0.4 & 0.9 & 0 \\
\end{bmatrix}
$$

