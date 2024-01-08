This project is part of Freecodecamp's [Scientific Computing with Python](https://www.freecodecamp.org/learn/scientific-computing-with-python/) curriculum

```py
class TreeNode:
    def __init__(self, key):
        # self: Which represents the instance of the class being created 
        # key: The value to be stored in the node
        self.key = key # Object instantiation
        self.left = None
        self.right = None

    def __str__(self):
        return str(self.key)

class BinarySearchTree:
    def __init__(self):
        self.root = None # The root attribute represents the root node of the binary search tree 

    def insert(self,key):
        self.root = self._insert(self.root, key)
        # self.root: Passes the root node of the tree as the first argument. This is the starting point for the insertion process
        # key: Passes the key value you want to insert as the second argument
        # _insert: Is a reference to a private method within the class that handles the actual insertion of the key into the data structure. It is marked as private by starting the method name with an underscore, indicating that it is intended to be used internally within the class and not accessed directly from outside the class
        
    def _insert(self, node, key):
        # Is a helper function and does the actual insertion. This method is recursive, meaning it calls itself to traverse the tree until the appropriate location for the new node is found
        
        if node is None:
            # If the node parameter is None, this means that the method has reached a leaf node or an empty spot in the tree where the new node should be inserted.

            return TreeNode(key)
        
            # Return TreeNode(key) to create a new TreeNode instance with the provided key. This will become the new leaf node, effectively inserting the key into the tree
        
        
        # Recursively traverse the tree and insert the values using the principle for binary trees:

        if key < node.key: # Values smaller than the key are placed in the left subtree
            node.left = self._insert(node.left, key) #  
        elif key > node.key: # Values greater than the key are placed in the right subtree
            node.right = self._insert(node.right, key)
        return node
        # After the insertion process is complete, return the current node to update the tree structure at the higher levels of the recursive call stack
            
    def search(self, key):
        return self._search(self.root, key)
        # self.root: This is the root of the binary search tree. The search starts from the root
        # key: This is the value that the user wants to find in the binary search tree
    
        # Internally, search delegates the actual search logic to the private _search method that performs the actual recursive search within the binary search tree
    
    def _search(self, node, key):
        if node is None or node.key == key: # Base case
            return node
        # If node is None: This indicates that the search has reached the end of a branch without finding the key
        # If node.key == key: This means that the key has been found in the current node

        if key < node.key: # If target key is less than the current node's key, 
            return self._search(node.left, key) # The search continues in the left subtree
        
        return self._search(node.right, key) # Otherwise in the search continues in the right subtree

    def delete(self, key):
        # key: is the value that the user wants to delete from the binary search tree
        self.root = self._delete(self.root, key) 
        # Deleting the node with the specified key will assign the result as the new root of the tree

    def _delete(self, node, key):
        if node is None: # When the current node is None, the key to be deleted was not found
            return node
        if key < node.key:
            node.left = self._delete(node.left, key)
        elif key > node.key:
            node.right = self._delete(node.right, key)
        # The above conditionals are valid for nodes with either zero or one child
        else:
            if node.left is None:
                return node.right
            
            elif node.right is None:
                return node.left  
            # If neither one of the previous conditions is met, it means the node has both left and right children
            
            # To choose the successor, you need to find the minimum value in the right subtree. The smallest value will be the in-order successor of the current node
            node.key = self._min_value(node.right)

            node.right = self._delete(node.right, node.key) 
            # Recursively delete the node with the minimum value from the right 

        return node 
    
        
    
    def _min_value(self, node):
        # When the node to be deleted has two children, we need to choose the replacement node from the children. The in-order successor method chooses the smallest element from the right subtree and places that element in place of the deleted node

        # To find the smallest value in the right subtree, iterate through the left children of the given node until the leftmost (smallest) node in the subtree has been reached. As long as there is a left child, the loop continues and there is a smaller value to be found.
        
        while node.left is not None:        
            node = node.left 
            # Once the leftmost node is found (that is, when node.left becomes None), the loop exits.
        
        return node.key # Replacement value
    

    # The inorder_traversal method is responsible for performing an in-order traversal of the binary search tree. It returns the keys of the nodes in sorted order. In-order traversal is a depth-first binary tree traversal algorithm that visits the left subtree, the current node, and then the right subtree.
    def inorder_traversal(self):
        result = []

        self._inorder_traversal(self.root, result) 
        # This will start the traversal from the root of the binary search tree (self.root), and the result list will be passed to accumulate the keys during the traversal.

        return result # Sorted list
    
    def _inorder_traversal(self, node, result):
        # node: is the current node being considered during the traversal
        # result: is the list to which the keys are appended in sorted order
        
        if node: # If node is not empty
            self._inorder_traversal(node.left, result) # Sorting the left children
            result.append(node.key) # Sorted values being added

            self._inorder_traversal(node.right, result) # Sorting the right children
            
bst = BinarySearchTree()

nodes = input('Input Nodes: ')

# nodes = [50, 30, 20, 40, 70, 60, 80]

# ---- Modified code ----

nodesArray = [int(node) for node in nodes.split()]

for node in nodesArray:
    bst.insert(node)

print("Inorder traversal:", bst.inorder_traversal())

searchNode = int(input('Node to be searched: '))

print(f"Search for {searchNode}:", 'Found' if bst.search(searchNode) else 'Not found')

deleteNode = int(input('Node to be deleted: '))

print('Node deleted' if bst.delete(deleteNode) is None else 'Node doesn\'t exist')

print(f"Inorder traversal after deleting {deleteNode}:", bst.inorder_traversal())

print(f"Search for {deleteNode}:", "Not found" if bst.search(deleteNode) is None else "Found")
            

# ---- Modified code ----
```