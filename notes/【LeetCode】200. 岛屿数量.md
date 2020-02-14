给定一个由 '1'（陆地）和 '0'（水）组成的的二维网格，计算岛屿的数量。一个岛被水包围，并且它是通过水平方向或垂直方向上相邻的陆地连接而成的。你可以假设网格的四个边均被水包围。

示例 1:

输入:
11110
11010
11000
00000

输出: 1
示例 2:

输入:
11000
11000
00100
00011

输出: 3

解法一:DFS
```
class Solution {
    int[][] direct = {{-1,0},{1,0},{0,1},{0,-1}};
    boolean[][] vis;
    int rows;
    int cols;
    
    public int numIslands(char[][] grid) {
        
         rows = grid.length;
         if(rows == 0) return 0;
         cols = grid[0].length;
        vis = new boolean[rows][cols];
        int count = 0;
        for(int i = 0; i < rows; i++){
            for(int j = 0; j < cols; j++){
                if(grid[i][j] == '1' && !vis[i][j]){
                    count++;
                    dfs(grid,i,j);
                }
            }
        }
        return count;
    }
    public void dfs(char[][] grid, int i,int j){
        vis[i][j] = true;
        for(int k = 0; k < 4; k++){
            int newX = i + direct[k][0];
            int newY = j + direct[k][1];
            if(inArea(newX, newY) && 
            grid[newX][newY] == '1' && !vis[newX][newY]){
                dfs(grid, newX, newY);
            }
        }
    }


    public boolean inArea(int i,int j){
        return i >=0 && i < rows && j >= 0 && j < cols;
    }
}
```

解法二:BFS
```
class Solution {
    int[][] direct = {{-1,0},{1,0},{0,1},{0,-1}};
    boolean[][] vis;
    int rows;
    int cols;
    
     public int numIslands(char[][] grid) {
        
         rows = grid.length;
         if(rows == 0) return 0;
         cols = grid[0].length;
        vis = new boolean[rows][cols];
        int count = 0;
        for(int i = 0; i < rows; i++){
            for(int j = 0; j < cols; j++){
                if(grid[i][j] == '1' && !vis[i][j]){
                    count++;
                    LinkedList<Integer> queue = new LinkedList<>();
                    queue.addLast(i * cols + j);
                    vis[i][j] = true;
                    while(!queue.isEmpty()){
                        int cur = queue.removeFirst();
                        int curX = cur / cols;
                        int curY = cur % cols;
                        for(int k = 0; k < 4; k++){
                            int newX = curX + direct[k][0];
                            int newY = curY + direct[k][1];
                            if(inArea(newX, newY) && grid[newX][newY] == '1' && !vis[newX][newY]){
                                     queue.addLast(newX * cols + newY);
                                     vis[newX][newY] = true;
                             }
                        }
                    }
                }
            }
        }
        return count;
    }


    public boolean inArea(int i,int j){
        return i >=0 && i < rows && j >= 0 && j < cols;
    }
}
```
