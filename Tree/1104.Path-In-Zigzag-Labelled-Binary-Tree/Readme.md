### 1104.Path-In-Zigzag-Labelled-Binary-Tree

本题的突破口是，如果是一棵按顺序横向排列的完全二叉树（即没有Zigzag），我们有这样的一个性质：任意label的节点，一路向上走到根节点的路径就是```label, label/2, label/2/2, label/2/2/2 ....````直至走到根节点0.

本题中，从label往上的过程中，每走一行，该行的节点编号种类其实不会变，但顺序/逆序会变化一下。举个例子，label是14，它位于第3层（以0-index计算）；那么第2层的节点编号一定是从4到7，或者从7到4. 不管是什么顺序，ZigZag会导致14的父节点一定不是7，而是7在该层的对称编号，即4. 

所以本题的算法是：最底层的初始节点是label，它的层级编号就是n = log2(label). 第n-1层的节点编号范围就是```pow(2, n-1)```到```pow(2, n) -1```。不管是否顺序逆序，label的父节点不是label/2，而是label/2在该行节点编号中的中轴对称位置。令p是label/2的对称位置，那么由对称性肯定有```label/2-pow(2,n-1) = pow(2,n)-1 - p```，即有```p = pow(2,n)-1 - label/2 + pow(2,n-1)```. 由此我们循环利用这个公式直至p的编号减至0.