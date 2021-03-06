这道题其实应该算是 Easy 难度的吧。

不过可以顺便复习一下 BST 的基本概念：

1. 左边所有子节点的值都要小于当前节点
2. 右边所有自节点的值都要大于当前节点
3. 左子树与右子树仍为 BST

背概念最没意思了，要知道 BST 的本质是对**二分搜索**思想在数据结构上的一种体现。
所以保持有序是基本条件，二叉树如何有序？左边永远小于右边。就是这么简单粗暴。

对于第三条，傻子应该都能听出其递归性的特征。

所以要验证是否为 BST，优先考虑递归解法。（另外一句话，十个二叉树，九个递归解。）

但这道题容易疏忽之处在于：由于其递归性，下一层的节点不仅要与当前节点比较，还应与当前节点的上层节点比较。

具体举例如下：

      4
     /^\
    1   7
       / \
      3   9
      ^

该树便不是 BST，因为第三层的节点值(3)小于根节点值(4)。从本质上讲，便是不符合有序的条件。

所以我们可以 suppose 每一个节点都应该有一个边界，即 min 与 max.
但稍稍验证，便可知，并非所有节点都有边界，如 1 与 9 便分别没有左边界与右边界。

有人会说，怎么没有，左边界是 INT_MIN，右边界是 INT_MAX。
这样的判断非常武断，不过可以提交试试，就知道 test case 有多么恶心了，哈哈。

所以我们的递归函数，必备的除了 min 与 max 外，应该增加两个 `bool` 值，记录是否存在左边界与右边界。

代码三行，不多说了。
