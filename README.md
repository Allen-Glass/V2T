# V2T
Voice-to-Text
public class
{
    private int[] iValues;
    private int iSize;
    
    /**
     * Default constructor. Creates an empty list.
     */
    public IntListVer3(){
        //redirect to single int constructor
        this(DEFAULT_CAP);
        //other statments could go here.
    }

    public IntListVer3(int initialCap) {
        assert initialCap > 0 : "Violation of precondition. IntListVer1(int initialCap):"
            + "initialCap must be greater than 0. Value of initialCap: " + initialCap;
        iValues = new int[initialCap];
        iSize = 0;
    }
    
     * Default add method. Add x to the end of this IntList.
     * Size of the list goes up by 1.
     * @param x The value to add to the end of this list.
     */
    public void add(int x){
        //example of loose coupling
        insert(iSize, x);
    }
    
    /**
     * Retrieve an element from the list based on position.
     * @param pos 0 <= pos < size()
     * @return The element at the given position.
     */
    public int get(int pos){
        assert 0 <= pos && pos < size() : "Failed precondition get. " +
        		"pos it out of bounds. Value of pos: " + pos;
        return iValues[pos];
    }
    
    /**
     * Insert x at position pos. Elements with a position equal
     * to pos or more are shifted to the right. (One added to their
     * position.)
     * post: get(pos) = x, size() = old size() + 1
     * @param pos 0 <= pos <= size()
     * @param x
     */
    public void insert(int pos, int x){
        assert 0 <= pos && pos <= size() : "Failed precondition insert. " +
        "pos is invalid. Value of pos: " + pos;
        ensureCapcity();
        for(int i = iSize; i > pos; i--){
            iValues[i] = iValues[i - 1];
        }
        iValues[pos] = x;
        iSize++;
    }
    
    /**
     * Remove an element from the list based on position.
     * Elements with a position greater than pos
     * are shifted to the left. (One subtracted from their
     * position.)
     * @param pos 0 <= pos < size()
     * @return The element that is removed.
     */
    public int remove(int pos){
        assert 0 <= pos && pos < size() : "Failed precondition remove. " +
        "pos it out of bounds. Value of pos: " + pos;
        int removedValue = iValues[pos];
        for(int i = pos; i < iSize - 1; i++)
            iValues[i] = iValues[i + 1];
        iSize--;
        return removedValue;
    }
    
    private void ensureCapcity(){
        // is there extra capacity available?
        // if not, resize
        if(iSize == iValues.length)
            resize();
    }
    
    /**
     * Returns the size of the list.
     * @return The size of the list.
     */
    public int size(){
        return iSize;
    }
    
    // resize internal storage container by a factor of 2
    private void resize() {
        int[] temp = new int[iValues.length * 2];
        System.arraycopy(iValues, 0, temp, 0, iValues.length);
        iValues = temp;
    }
    
    /**
     * Return a String version of this list. Size and 
     * elements included.
     */
    public String toString(){
        // we could make this more effecient by using a StringBuffer.
        // See alternative version
        String result = "size: " + iSize + ", elements: [";
        for(int i = 0; i < iSize - 1; i++)
            result += iValues[i] + ", ";
        if(iSize > 0 )
            result += iValues[iSize - 1];
        result += "]";
        return result;
    }
    
    // Would not really have this and toString available
    // both included just for testing
    public String toStringUsingStringBuffer(){
        StringBuffer result = new StringBuffer();
        result.append( "size: " );
        result.append( iSize );
        result.append(", elements: [");
        for(int i = 0; i < iSize - 1; i++){
            result.append(iValues[i]);
            result.append(", ");
        }
        if( iSize > 0 )
            result.append(iValues[iSize - 1]);
        result.append("]");
        return result.toString();
    }
}
