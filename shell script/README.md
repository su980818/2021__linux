# 2263
https://www.acmicpc.net/problem/2263

![화면 캡처 2021-02-17 132911](https://user-images.githubusercontent.com/78835559/108156843-c4d53300-7124-11eb-8d32-a195c86b86e0.png)

post order 의 마지막 부분을 보고 root 를 알아 낼수 있고 
inorder에서는 이를 이용해 두개의 subtree를 분리할수 있음.

이과정을 반복하여 트리를 재구성 할수 있을꺼 같음. 
preorder 은 root 출력 -> left_subtree 출력 -> right_subtree출력 임으로 위의 과정에서 root , left_subtree , right_subtree를 모두 알수 있기 때문에 문제를 풀수있음 



*처음 inorder의 subtree 구역과 postorder의 subtree구역을 동일하게 생각하여 문제 발생 
