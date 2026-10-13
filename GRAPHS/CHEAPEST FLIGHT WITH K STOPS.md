```java
class Pair {
    int node, price, stops;
    Pair(int node, int price, int stops) {
        this.node = node;
        this.price = price;
        this.stops = stops;
    }
}

class Solution {
    public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
        List<List<Pair>> adjList = new ArrayList<>();
        for (int i = 0; i < n; i++) adjList.add(new ArrayList<>());
        for (int[] flight : flights) {
            adjList.get(flight[0]).add(new Pair(flight[1], flight[2], 0));
        }

        PriorityQueue<Pair> pq = new PriorityQueue<>((a, b) -> Integer.compare(a.price, b.price));
        pq.add(new Pair(src, 0, 0));

        while (!pq.isEmpty()) {
            Pair curr = pq.poll();
            if (curr.node == dst) return curr.price;
            if (curr.stops > k) continue;

            for (Pair nei : adjList.get(curr.node)) {
                pq.add(new Pair(nei.node, curr.price + nei.price, curr.stops + 1));
            }
        }
        return -1;
    }
}

```
## INTUTION 
* HAVE A COUNT ON THE PRICE AND NO.OF STOPS OF THE FLIGHTS.
* ADD THEM TO A PRIORITY QUEUE WHICH COMPARES THE PRICES.
* RUN DJIKSTRA ON THE GRAPH.
* IF A FLIGHT HAS STOPS MORE THAN THE THRESHOLD, SKIP THE LOOP AND DONT ADD IT TO THE PRIORITY QUEUE.
* THE MOMENT YOU FIND THE DESTINATION NODE RETURN THE PRICE.