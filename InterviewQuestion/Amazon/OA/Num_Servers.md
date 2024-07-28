


![题目](IMG_4518.JPG)
![题目](IMG_4519.JPG)
![题目](IMG_4520.JPG)
![题目](IMG_4521.JPG)
![题目](IMG_4522.JPG)


public static List<Integer> getServerIds(int num_servers, List<Integer> requests) {

    int len = requests.length();
    int[] serverLoads = new int[num_servers]; // 这是建立 了一个 server 的列表，然后 就是在这个列表上更改 ， 改了那个 index， 然后把这个index 加到 result 里面，这个就是答案的组成
    int[] result = new int[len];

    for(int i = 0; i < len; i++>) {
        int minLoad = Integer.MAX_VALUE;
        int serverId = -1;

        for( int j = 0; j <= requests.get[i]; j++) {
            if (serverLoads[j] < minLoad>) {
                minLoad = serverLoads[j];
                serverId = j;
            }
        }

        result[i] = serverId;
        serverLoads[serverId]++;

    }

    return result;
    
}