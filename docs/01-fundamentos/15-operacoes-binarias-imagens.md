# Operações Binárias Induzidas por Operações Unárias

## Introdução

![Operações binárias induzidas](../assets/images/op-bin-imagens-1.png)

As mesmas funções que induzem **operações unárias** podem também induzir as **binárias**.

---

## Exponenciação de Imagens

Seja a função exponencial \( f : \mathbb{R}^{\geq 0} \rightarrow \mathbb{R} \) definida por \( f(r) = r^k \), sendo \( k \) um real não-negativo.

Esta função induz a operação unária:

\[
\mathbf{a}^k = \{(\mathbf{x}, \mathbf{b}(\mathbf{x})) : \mathbf{b}(\mathbf{x}) = [\mathbf{a}(\mathbf{x})]^k, \mathbf{x} \in \mathbf{X}\}
\]

### Extensão para Operação Binária

![Operação binária exponencial](../assets/images/op-bin-imagens-2.png)

Se \( \mathbf{a}, \mathbf{b} \in (\mathbb{R}^{\geq 0})^{\mathbf{X}} \), esta pode então ser estendida para a seguinte operação binária:

\[
\mathbf{a}^{\mathbf{b}} = \{(\mathbf{x}, \mathbf{c}(\mathbf{x})) : \mathbf{c}(\mathbf{x}) = \mathbf{a}(\mathbf{x})^{\mathbf{b}(\mathbf{x})}\}
\]

### Logaritmo de Imagens

Definimos logaritmo similarmente:

\[
\log_{\mathbf{b}} \mathbf{a} = \{(\mathbf{x}, \mathbf{c}(\mathbf{x})) : \mathbf{c}(\mathbf{x}) = \log_{\mathbf{b}(\mathbf{x})} \mathbf{a}(\mathbf{x})\}
\]

---

## Pseudo-Inversa

![Pseudo-inversa](../assets/images/op-bin-imagens-3.png)

Por fim, como tais operações podem levar a **valores indeterminados** como divisões por zero, a álgebra de imagens permite a definição de uma **pseudo-inversa**:

\[
\mathbf{a}^{-1} = \{(\mathbf{x}, \mathbf{b}(\mathbf{x})) : \mathbf{b}(\mathbf{x}) = \frac{1}{\mathbf{a}(\mathbf{x})} \text{ se } \mathbf{a}(\mathbf{x}) \neq 0, \mathbf{b}(\mathbf{x}) = 0 \text{ caso contrário}\}
\]

!!! warning "Tratamento de Zero"
    A pseudo-inversa evita divisão por zero atribuindo 0 aos pixels onde \( \mathbf{a}(\mathbf{x}) = 0 \).

---

## Exemplos Matriciais

![Exemplos matriciais](../assets/images/op-bin-imagens-4.png)

Considere as imagens \( \mathbf{a} \) e \( \mathbf{b} \) representadas pelas matrizes:

\[
A = \begin{bmatrix} 4 & 1 & -1 \\ 3 & 5 & 2 \\ 1 & -4 & 6 \end{bmatrix} \qquad B = \begin{bmatrix} 1 & 1 & -1 \\ 2 & 0 & 3 \\ -1 & 2 & 0 \end{bmatrix}
\]

### Soma \( \mathbf{c} = \mathbf{a} + \mathbf{b} \)

\[
C = \begin{bmatrix} 5 & 2 & -2 \\ 5 & 5 & 5 \\ 0 & -2 & 6 \end{bmatrix}
\]

### Exponenciação \( \mathbf{c} = \mathbf{a}^{\mathbf{b}} \)

\[
C = \begin{bmatrix} 4 & 1 & -1 \\ 9 & 1 & 8 \\ 1 & 16 & 1 \end{bmatrix}
\]

!!! note "Cálculo"
    - \( 4^1 = 4, 1^1 = 1, (-1)^{-1} = -1 \)
    - \( 3^2 = 9, 5^0 = 1, 2^3 = 8 \)
    - \( 1^{-1} = 1, (-4)^2 = 16, 6^0 = 1 \)

---

## Código MATLAB: Pseudo-Inversa

![Código pseudo-inversa](../assets/images/op-bin-imagens-5.png)

```matlab
clear;
img = imread('barbara.png'); img = double(img); img = img/255;
[nl, nc] = size(img);
for i = 1:nl
    for j = 1:nc
        if img(i, j) ~= 0
            img2(i, j) = 1/img(i, j);
        else
            img2(i, j) = 0;
        end
    end
end
img2 = img2/max(img2(:));  % normalização
imshow(img2);
```

!!! tip "Normalização"
    A normalização final (`img2/max(img2(:))`) é necessária pois a inversa pode gerar valores muito altos onde \( \mathbf{a}(\mathbf{x}) \) é muito pequeno.

### Resultado Visual

![Resultado pseudo-inversa](../assets/images/op-bin-imagens-6.png)

| Imagem | Descrição |
|--------|-----------|
| **a** (Original) | Imagem Barbara |
| **a⁻¹** (Inversa) | Regiões claras ficam escuras e vice-versa |

---

## Resumo

| Operação | Notação | Definição |
|----------|---------|-----------|
| **Exponenciação unária** | \( \mathbf{a}^k \) | \( [\mathbf{a}(\mathbf{x})]^k \) |
| **Exponenciação binária** | \( \mathbf{a}^{\mathbf{b}} \) | \( \mathbf{a}(\mathbf{x})^{\mathbf{b}(\mathbf{x})} \) |
| **Logaritmo** | \( \log_{\mathbf{b}} \mathbf{a} \) | \( \log_{\mathbf{b}(\mathbf{x})} \mathbf{a}(\mathbf{x}) \) |
| **Pseudo-inversa** | \( \mathbf{a}^{-1} \) | \( 1/\mathbf{a}(\mathbf{x}) \) ou 0 |
