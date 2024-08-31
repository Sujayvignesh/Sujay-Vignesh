import java.util.ArrayList;
import java.util.List;

public class TextJustification {

    public List<String> fullJustify(String[] words, int maxWidth) {
        List<String> result = new ArrayList<>();
        int index = 0;

        while (index < words.length) {
            int lineLength = words[index].length();
            int last = index + 1;

            while (last < words.length && lineLength + words[last].length() + (last - index) <= maxWidth) {
                lineLength += words[last].length();
                last++;
            }

            StringBuilder line = new StringBuilder();
            int numWords = last - index;
            int numSpaces = maxWidth - lineLength;

            if (last == words.length || numWords == 1) {
                for (int i = index; i < last; i++) {
                    line.append(words[i]);
                    if (i < last - 1) line.append(" ");
                }
                while (line.length() < maxWidth) {
                    line.append(" ");
                }
            } else {
                int spacesBetweenWords = numSpaces / (numWords - 1);
                int extraSpaces = numSpaces % (numWords - 1);

                for (int i = index; i < last; i++) {
                    line.append(words[i]);
                    if (i < last - 1) {
                        for (int j = 0; j <= spacesBetweenWords + (i - index < extraSpaces ? 1 : 0); j++) {
                            line.append(" ");
                        }
                    }
                }
            }

            result.add(line.toString());
            index = last;
        }

        return result;
    }

    public static void main(String[] args) {
        TextJustification tj = new TextJustification();
        String[] words = {"This", "is", "an", "example", "of", "text", "justification."};
        int maxWidth = 16;

        List<String> result = tj.fullJustify(words, maxWidth);
        for (String line : result) {
            System.out.println("\"" + line + "\"");
        }
    }
}
