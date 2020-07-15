---
layout: post
title: "[Everyday Programming]매일프로그래밍 #18"
description: >
    이진 트리 좌우 대칭 반전하기
author: Yunmin Cho
tags: [EverydayProgramming]
category: [Algorithm]
---

❓__문제__❓  
이진 트리를 루트 노드를 기준으로 좌우반전 하시오.  
이 문제는 구글이 Homebrew 창시자에게 낸 문제로 유명합니다.  

<br/>

❓__Question__❓  
Given a binary tree root node, reverse the tree horizontally.  
* * *
❗__풀이__❗  
문제를 풀려면 이진 트리가 당연히 필요하다.  
그래서 이진 트리 구현부터 시작했다!  

노드를 나타내는 TreeNode 클래스와, 노드를 역어서 만든 tree를 관리하는 BTree 클래스를 만들었다. 이진 트리에 대한 규칙이 없어 임의로 Binary Tree로 구현했다.  

~~~c++
template <typename T>
class BTree;

template <typename T>
class TreeNode {
	friend class BTree<T>;
private:
	TreeNode* left;
	T data;
	TreeNode* right;
public:
	TreeNode(T input = 0, TreeNode* left = NULL, TreeNode* right = NULL) {
		data = input;
		this->left = left;
		this->right = right;
	}
	~TreeNode() {}
};

template <typename T>
class BTree {
private:
	TreeNode<T>* root;
	void print(TreeNode<T>* node); // 재귀로 트리 출력
public:
	BTree() {};
	~BTree() {};

	TreeNode<T>* GetRoot() { return root; }
	void SetRoot(T input) { root = new TreeNode<T>(input); return; }
	void InputNewData(T input, TreeNode<T>* node); // 재귀로 알맞은 위치 찾아서 데이터 입력
	void PrintTree(); // 외부에서 호출 가능한 출력 함수
	void ReverseTree(TreeNode<T>* node); // 트리 좌우 반전
};
~~~

GetRoot와 SetRoot는 inline 함수로 구현했지만, 나머지는 재귀함수이기 때문에, 클래스 외부에 정의했다.  

가장 중요한 ReverseTree는 Tree를 좌우반전 하는 함수이다.  
알고리즘은 간단하다. <span style="color: var(--highlight-color)">노드를 순회하면서, 좌우 포인터를 바꾸어주면 된다.</span>  

현재 노드 기준 좌우 포인터를 바꾼 후 왼쪽 노드, 오른쪽 노드 순으로 방문해서 똑같이 좌우 포인터를 바꾸어준다. 재귀함수로 모든 노드를 순회하며 좌우 뒤집기!  
~~~c++
template <typename T>
void BTree<T>::ReverseTree(TreeNode<T>* node) {
	if (node->left != NULL || node->right != NULL) { // 왼쪽 오른쪽 하나라도 가리키는 노드가 있으면 자리 바꾸기
		TreeNode<T>* temp;
		temp = node->right;
		node->right = node->left;
		node->left = temp;
	}

	if (node->left != NULL) {
		ReverseTree(node->left);
	}
	if (node->right != NULL) {
		ReverseTree(node->right);
	}

	return;
}
~~~

전체 코드는 아래와 같다. `BTree.h`와 `main.cpp`  
__BTree.h__
~~~c++
#pragma once

template <typename T>
class BTree;

template <typename T>
class TreeNode {
	friend class BTree<T>;
private:
	TreeNode* left;
	T data;
	TreeNode* right;
public:
	TreeNode(T input = 0, TreeNode* left = NULL, TreeNode* right = NULL) {
		data = input;
		this->left = left;
		this->right = right;
	}
	~TreeNode() {}
};

template <typename T>
class BTree {
private:
	TreeNode<T>* root;
	void print(TreeNode<T>* node); // 재귀로 트리 출력
public:
	BTree() {};
	~BTree() {};

	TreeNode<T>* GetRoot() { return root; }
	void SetRoot(T input) { root = new TreeNode<T>(input); return; }
	void InputNewData(T input, TreeNode<T>* node); // 재귀로 알맞은 위치 찾아서 데이터 입력
	void PrintTree(); // 외부에서 호출 가능한 출력 함수
	void ReverseTree(TreeNode<T>* node); // 트리 좌우 반전
};

template <typename T>
void BTree<T>::InputNewData(T input, TreeNode<T>* node) {
	if (node->data >= input) {
		if (node->left == NULL) { // 왼쪽이 비었으면 새 노드 추가
			node->left = new TreeNode<T>(input);
		}
		else
			InputNewData(input, node->left);
	}
	else {
		if (node->right == NULL) { // 오른쪽이 비었으면 새 노드 추가
			node->right = new TreeNode<T>(input);
		}
		else
			InputNewData(input, node->right);
	}
	return;
}

template <typename T>
void BTree<T>::print(TreeNode<T>* node) {
	std::cout << node->data << " ";
	if (node->left != NULL)
		print(node->left);
	if(node->right != NULL)
		print(node->right);
	return;
}

template <typename T>
void BTree<T>::PrintTree() {
	std::cout << "전위 순회 (Preorder) 출력: ";
	print(root);
	std::cout << std::endl;
	return;
}

template <typename T>
void BTree<T>::ReverseTree(TreeNode<T>* node) {
	if (node->left != NULL || node->right != NULL) { // 왼쪽 오른쪽 하나라도 가리키는 노드가 있으면 자리 바꾸기
		TreeNode<T>* temp;
		temp = node->right;
		node->right = node->left;
		node->left = temp;
	}

	if (node->left != NULL) {
		ReverseTree(node->left);
	}
	if (node->right != NULL) {
		ReverseTree(node->right);
	}

	return;
}
~~~

__main.cpp__
~~~c++
#include <iostream>
#include "BTree.h"
using namespace std;

int main() {
	BTree<int> tree;

	int count = 0;
	cout << "Input Tree data as you want: ";
	do {
		int temp;
		cin >> temp;

		if (count == 0) {
			tree.SetRoot(temp);
			count++;
		}
		else {
			tree.InputNewData(temp, tree.GetRoot());
		}
	} while (getc(stdin) == ' ');

	cout << "<Before>" << endl;
	tree.PrintTree();

	tree.ReverseTree(tree.GetRoot());
	cout << "<After>" << endl;
	tree.PrintTree();

	system("pause");
	return 0;
}
~~~

*문제 출처 - 2019매일프로그래밍*