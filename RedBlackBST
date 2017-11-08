#include <iostream>
using namespace std;
#include <stack>
bool RED = true;
bool BLACK = false;

class Node
{//add the color property
	int key;
	char value;
	Node *lchild;
	Node *rchild;
	int count;
	bool color;
	
	Node(int key, int value, int n, bool color)
	{
		this->key = key;
		this->value = value;
		this->count = n;
		this->color = color;
		lchild = NULL;
		rchild = NULL;
	}
	bool isRed(Node *cur)
	{
		if (cur == NULL)
			return false;
		return cur->color == RED;
	}
	friend class BST;
};

class BST
{
private:
	Node *root;
	BST()
	{
		root = NULL;
	}
	int size(Node *cur);
	Node* rotateLeft(Node *cur);//rotate left
	Node* rotateRight(Node *cur);//rotate right

	char get(Node *cur, int k);
	//search
	Node* put(Node *cur, int k, char v);
	//insert

	Node* min(Node *cur);
	//get the min member
	Node* max(Node *cur);
	//get the max member
	void flipColors(Node *cur);
	//increase the height of the tree

	Node* floor(Node *cur, int k);
	//get the member equal to or less than k
	Node* celling(Node *cur, int k);
	//get the member equal to or greater than k

	Node* select(Node *cur, int k);
	//return the key which rank is k
	int rank(Node *cur, int k);
	//return the rank of the key which key is k
	
	Node* delmin(Node *cur);
	Node* delmax(Node *cur);
	Node* Delete(Node *cur, int k);//delete the member which key = k
};

int BST::size(Node *cur)
{
	if (cur == NULL)
		return 0;
	else
		return cur->count;
}

Node* BST::rotateLeft(Node *cur)
{
	Node *x = cur->rchild;
	cur->rchild = x->lchild;
	x->lchild = cur;
	//change color
	x->color = cur->color;
	cur->color = RED;
	//change count
	x->count = cur->count;
	cur->count = size(cur->rchild) + size(cur->lchild) + 1;
	return cur;
}

Node* BST::rotateRight(Node *cur)
{
	Node *x = cur->lchild;
	cur->lchild = x->rchild;
	x->rchild = cur;
	//change color
	x->color = cur->color;
	cur->color = RED;
	//change count
	x->count = cur->count;
	cur->count = size(cur->lchild) + size(cur->rchild) + 1;
	return cur;
}

void BST::flipColors(Node *cur)
{
	cur->color = RED;
	cur->rchild->color = BLACK;
	cur->lchild->color = BLACK;
}







char BST::get(Node *cur, int k)
{
	if (cur == NULL)
		return NULL;
	if (cur->key < k)
		return get(cur->lchild, k);
	else if (cur->key > k)
		return get(cur->rchild, k);
	else
		return cur->value;
}

Node* BST::put(Node *cur, int k, char v)
{
	if (cur == NULL)
		cur = new Node(k, v, 1,RED);

	if (cur->key > k)
		cur->lchild = put(cur->lchild, k, v);
	else if (cur->key < k)
		cur->rchild = put(cur->rchild, k, v);
	else
		cur->value = v;

	if (isRed(cur->lchild) && !isRed(cur->lchild)) 
		cur = rotateLeft(cur);
	if (isRed(cur->lchild) && isRed(cur->lchild->lchild))
		cur = rotateRight(cur);
	if (isRed(cur->lchild) && isRed(cur->rchild))
		flipColors(cur);



	cur->count = size(cur->lchild) + size(cur->rchild) + 1;
	return cur;
}

Node* BST::min(Node *cur)
{
	if (cur->lchild != NULL)
		return min(cur->lchild);
	return cur;
}
Node* BST::max(Node *cur)
{
	if (cur->lchild != NULL)
		return max(cur->rchild);
	return cur;
}
Node* BST::floor(Node *cur, int k)
{
	if (cur == NULL)
		return NULL;
	if (cur->key == k)
		return cur;
	if (cur->key > k && cur->lchild)
		return floor(cur->lchild, k);
	Node *t = floor(cur->rchild, k);
	if (t == NULL)
		return cur;
	return t;
}

Node* BST::select(Node *cur, int k)
{
	if (cur == NULL)
		return NULL;
	int num = cur->lchild->count;
	if (k < num + 1)
		return select(cur->lchild, k);
	else if (k > num + 1)
		return select(cur->rchild, k - num - 1);
	else
		return cur;
}

int BST::rank(Node *cur, int k)
{
	if (cur == NULL)
		return 0;
	if (k <cur->key)
		return rank(cur->lchild, k);
	else if (k > cur->key)
		return rank(cur->rchild, k) + 1 +size(cur->lchild);
	else
		return size(cur->lchild) + 1;
}
Node* BST::delmin(Node *cur)
{
	if (cur->lchild == NULL)
		return cur->rchild;
	cur->lchild = delmin(cur->lchild);
	cur->count = size(cur->lchild) + size(cur->rchild) + 1;
	return cur;
}

Node* BST::delmax(Node *cur)
{
	if (cur->rchild == NULL)
		return cur->lchild;
	cur->rchild = delmax(cur->rchild);
	cur->count = size(cur->lchild) + size(cur->rchild) + 1;
	return cur;
}

Node* BST::Delete(Node *cur, int k)
{//delete the key is k
	if (cur == NULL)
		return NULL;

	if (k < cur->key)
		Delete(cur->lchild, k);
	else if (k > cur->key)
		Delete(cur->rchild, k);
	else {
	if (cur->rchild == NULL)
		return cur->lchild;
	if (cur->lchild == NULL)
		return cur->lchild;
	Node *t = cur;
	cur = min(cur->rchild);
	cur->lchild = t->lchild;
	cur->rchild = delmin(t->rchild);
	}
	cur->count = size(cur->lchild) + size(cur->rchild) + 1;
	return cur;
};





