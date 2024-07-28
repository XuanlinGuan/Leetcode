
![](IMG_4523.JPG)
![](IMG_4524.JPG)
![](IMG_4525.JPG)
![](IMG_4526.JPG)
![](IMG_4527.JPG)


public static int getMaxTotalArea(List<Integer> sideLengths) {

    System.out.println(sideLenghts);
    Collections.sort(sideLengths);

    long length = 0;
    long sumArea = 0;
    int MOD = 100000007;

    int i = sideLengths.size() - 1;
    while(i > 0) {
        if (Math.abs(sideLengths.get(i) - sideLengths.get(i-1)) <= 1) {
            if (length == 0) {
                length = Math.min(sideLengths.get(i), sideLengths.get(i-1));
                i -= 1;
            } else {
                sumArea += length * Math.min(sideLengths.get(i), sideLengths.get(i-1));
                sumArea %= MOD;
                i -= 1;
                length = 0;
            }
        }
        i -= 1;
    }
    return (int)sumArea;
}