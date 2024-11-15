# Алгоритм Дейкстры на Python

Алгоритм Дейкстры используется для поиска кратчайшего пути от одной вершины графа к другим вершинам в графе с неотрицательными весами ребер. В этом репозитории представлена реализация алгоритма на Python с использованием очереди с приоритетом (heapq).

## Описание алгоритма

Алгоритм Дейкстры инициализирует расстояния от стартовой вершины до всех других вершин как бесконечные (inf), кроме самой стартовой вершины, для которой расстояние равно 0. Затем он поочередно обновляет минимальные расстояния до соседних вершин, пока не будет обработан весь граф.

## Структура данных

Граф представлен в виде словаря, где каждая вершина указывает на соседей и вес ребра до них.

Пример структуры графа:

graph = {
    'A': {'B': 1, 'C': 4},
    'B': {'A': 1, 'C': 2, 'D': 5},
    'C': {'A': 4, 'B': 2, 'D': 1},
    'D': {'B': 5, 'C': 1}
}

## Код

import heapq

def dijkstra(graph, start):
    # Инициализация расстояний до всех вершин как бесконечность
    distances = {vertex: float('inf') for vertex in graph}
    distances[start] = 0  # Расстояние до стартовой вершины равно 0
    # Очередь с приоритетом для выбора вершины с наименьшим расстоянием
    priority_queue = [(0, start)]
    
    while priority_queue:
        # Получаем вершину с минимальным расстоянием
        current_distance, current_vertex = heapq.heappop(priority_queue)
        
        # Если найдено большее расстояние, пропускаем
        if current_distance > distances[current_vertex]:
            continue
        
        # Обновляем расстояния до соседей
        for neighbor, weight in graph[current_vertex].items():
            distance = current_distance + weight
            
            # Если найден более короткий путь к соседу
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(priority_queue, (distance, neighbor))
    
    return distances

## Параметры

 * graph: Словарь, представляющий граф. Ключи — это вершины, а значения — словари соседних вершин и весов рёбер.
 * start: Вершина, с которой начинается поиск кратчайшего пути.

## Возвращаемое значение

Функция dijkstra возвращает словарь, где ключи — вершины графа, а значения — минимальные расстояния от стартовой вершины до соответствующих вершин.

## Пример использования

graph = {
    'A': {'B': 1, 'C': 4},
    'B': {'A': 1, 'C': 2, 'D': 5},
    'C': {'A': 4, 'B': 2, 'D': 1},
    'D': {'B': 5, 'C': 1}
}

start_vertex = 'A'
distances = dijkstra(graph, start_vertex)
print(distances)

## Ожидаемый вывод

{'A': 0, 'B': 1, 'C': 3, 'D': 4}

## Как работает алгоритм

 1. Инициализация: Задаем начальные расстояния до всех вершин как inf, кроме стартовой вершины, для которой расстояние — 0.
 2. Очередь с приоритетом: Используем heapq для хранения вершин с их текущими расстояниями, чтобы на каждом шаге доставать вершину с минимальным расстоянием.
 3. Основной цикл: Пока очередь не пуста, извлекаем вершину с наименьшим расстоянием и обновляем расстояния до её соседей.
 4. Возвращение результата: После завершения алгоритма возвращаем словарь с кратчайшими расстояниями до всех вершин от стартовой вершины.

## Сложность алгоритма

Сложность алгоритма составляет O(ElogV), где:

 * E  — количество рёбер,
 * V — количество вершин.

## Требования

Python 3.6 или выше.