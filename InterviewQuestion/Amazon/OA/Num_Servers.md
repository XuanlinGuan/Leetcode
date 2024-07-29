![题目](IMG_4518.JPG)
![题目](IMG_4519.JPG)
![题目](IMG_4520.JPG)
![题目](IMG_4521.JPG)
![题目](IMG_4522.JPG)


// "static void main" must be defined in a public class.
public class Main {
    public static void main(String[] args) {
        
        List<Integer> input = new ArrayList<>();
        // input.add(4);
        // input.add(0);
        // input.add(2);
        // input.add(2);
        
        input.add(3);
        input.add(2);
        input.add(3);
        input.add(2);
        input.add(4);
        
        List<Integer> ans = getServerIds(5,input);
        
        for(int i = 0; i < ans.size(); i++) {
            System.out.println(ans.get(i));   
        }
    }
    
    private static List<Integer> getServerIds(int num_servers, List<Integer> request) {
    int [] servers = new int[num_servers];
    int len = request.size();
    List<Integer> res = new ArrayList<>();
    for(int i = 0; i < len; i++) {
        int n = request.get(i);
        int minLoad = Integer.MAX_VALUE;
        int activeId = -1;
        for(int j = 0; j <= n; j++) {            
            if(servers[j] < minLoad ) {
                minLoad = servers[j];
                activeId = j;
            }
        }
        res.add(activeId);
        servers[activeId]++;
    }
    return res;
    }
}


	•	时间复杂度: O(n * num_servers)
	•	空间复杂度: O(num_servers + n)





优化： 
import java.util.ArrayList;
import java.util.List;
import java.util.PriorityQueue;

public class Main {
    public static void main(String[] args) {
        List<Integer> input = new ArrayList<>();
        input.add(4);
        input.add(0);
        input.add(2);
        input.add(2);

        List<Integer> ans = getServerIds(5, input);

        for (int i = 0; i < ans.size(); i++) {
            System.out.println(ans.get(i));
        }
    }

    private static List<Integer> getServerIds(int num_servers, List<Integer> request) {
        PriorityQueue<Server> minHeap = new PriorityQueue<>();
        for (int i = 0; i < num_servers; i++) {
            minHeap.offer(new Server(i, 0));
        }

        List<Integer> res = new ArrayList<>();
        for (int req : request) {
            // Temporary list to hold servers that need to be reinserted into the heap
            List<Server> temp = new ArrayList<>();
            Server minServer = null;

            // Find the server with the minimum load in the range [0, req]
            for (int j = 0; j <= req; j++) {
                Server server = minHeap.poll();
                temp.add(server);
                if (minServer == null || server.load < minServer.load || (server.load == minServer.load && server.id < minServer.id)) {
                    minServer = server;
                }
            }

            // Reinsert servers back into the heap
            for (Server server : temp) {
                if (server.id != minServer.id) {
                    minHeap.offer(server);
                }
            }

            // Assign the request to the selected server
            minServer.load++;
            res.add(minServer.id);
            minHeap.offer(minServer);
        }
        return res;
    }

    static class Server implements Comparable<Server> {
        int id;
        int load;

        Server(int id, int load) {
            this.id = id;
            this.load = load;
        }

        @Override
        public int compareTo(Server other) {
            if (this.load != other.load) {
                return this.load - other.load;
            } else {
                return this.id - other.id;
            }
        }
    }
}