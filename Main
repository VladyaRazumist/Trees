using System;
using System.Collections.Generic;
using System.Linq;

public class TreeNode<T>
{
    private readonly T _value;
    private readonly List<TreeNode<T>> _children = new List<TreeNode<T>>();

    public TreeNode(TreeNode<T> tn)
    {
        var node = new List<TreeNode<T>>(tn.Children);
        _children = node;
    }
    public TreeNode(T value)
    {
        _value = value;
    }

    public TreeNode<T> this[int i]
    {
        get { return _children[i]; }
    }

    public TreeNode<T> Parent { get; private set; }

    public T Value { get { return _value; } }

    public List<TreeNode<T>> Children
    {
        get { return _children; }
    }

    public TreeNode<T> AddChild(T value)
    {
        var node = new TreeNode<T>(value) { Parent = this };
        _children.Add(node);
        return node;
    }

    public TreeNode<T>[] AddChildren(params T[] values)
    {
        return values.Select(AddChild).ToArray();
    }

    public bool RemoveChild(TreeNode<T> node)
    {
        return _children.Remove(node);
    }

    public void Traverse(Action<T> action)
    {
        action(Value);
        foreach (var child in _children)
            child.Traverse(action);
    }

    public IEnumerable<T> Flatten()
    {
        return new[] { Value }.Concat(_children.SelectMany(x => x.Flatten()));
    }
}
public class Tree
{
    private Random rnd=new Random();
    
    private int maxChildren;
    private int currentNode=1;
    private int currentDepth = -1;
    private int depth = 3;
    private readonly TreeNode<int> top = new TreeNode<int> (1);
    public Tree() : this(3, 5)
    {
    }
    public Tree(int depth, int maxChildren)
    {
        this.depth = depth;
        this.maxChildren = maxChildren;
    }
    public void GenerateTree()
    {
        TreePath(top);
    }
    private void TreePath(TreeNode<int> tn)
    {
   
        currentDepth++;
        if (currentDepth < depth)
        {
            for (int i = 0; i < maxChildren; i++)
            {
                currentNode++;
                
                var t = tn.AddChild(currentNode);
                TreePath(t);
                currentDepth--;
            }
        }
    }
    public void DepthView()
    {
        Console.WriteLine();
        Console.WriteLine("DepthView");
        Console.WriteLine();
        Console.Write($"{top.Value}  ");
        DL(top);
    }
    private void DL(TreeNode<int> tn)
    {
        foreach (var item in tn.Children)
        {
            Console.Write($"{item.Value}  ");
            if (item.Children != null)
            {
                DL(item);
            }
        }
    }
    public void WidthView()
    {
        Console.WriteLine();
        Console.WriteLine("WidthView");
        Console.WriteLine();
        Console.Write($"{top.Value}  ");
        WL(top);
      
    }
    private void WL(TreeNode<int> tn)
    {
        foreach (var item in tn.Children)
        {
            Console.Write($"{item.Value}  ");
        }
        foreach (var item in tn.Children)
        {
            WL(item);
        }
    }
}


class Program
{
    static void Main(string[] args)
    {
        var tree = new Tree(depth:3,maxChildren:4);
        tree.GenerateTree();
        tree.WidthView();
        tree.DepthView();
        Console.ReadKey();
    }
}
