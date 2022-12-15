# A* algorithm
A* search algorithm written in C++ programming language.
 - requires compiler support for C++11

## algorithm theory

[算法原理介绍](https://github.com/hanlin-cheng/slam-study-note/blob/master/slam_theory/%E8%B7%AF%E5%BE%84%E8%A7%84%E5%88%92%E4%B9%8BA-star%E7%AE%97%E6%B3%95.md)

## Usage example
```cpp
#include <iostream>
#include "AStar.hpp"

int main() {
    //初始化地图，用二维矩阵代表地图，1表示障碍物，0表示可通
    std::vector<std::vector<int>> map = {{1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1},
                                         {1, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 1},
                                         {1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 1},
                                         {1, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 1},
                                         {1, 1, 1, 0, 0, 0, 0, 0, 1, 1, 0, 1},
                                         {1, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1},
                                         {1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 1},
                                         {1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1}};
    Astar astar;
    astar.InitAstar(map);

    //设置起始和结束点
    Point start(1, 1);
    Point end(6, 10);

    // A*算法找寻路径
    std::list<Point *> path = astar.GetPath(start, end, false);

    // 打印结果
    for (auto &p : path) {
        std::cout << "(" << p->x << "," << p->y << ") ";
    }
    std::cout << "\n";

    for (int row = 0; row < map.size(); ++row) {
        for (int col = 0; col < map[0].size(); ++col) {
            if (InPath(row, col, path)) {
                if (map[row][col] != 0) {
                    std::cout << "e ";
                } else {
                    std::cout << "* ";
                }
            } else {
                std::cout << map[row][col] << " ";
            }
        }
        std::cout << "\n";
    }
    return 0;
}
```

> 冰泉冷涩弦凝绝，凝绝不通声暂歇。别有幽愁暗恨生，此时无声胜有声。