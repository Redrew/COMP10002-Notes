# KMP!

        #include <stdio.h>

        int kmp(char *text, char *target, int failure_array[])
        {
                int start = 0, cur = 0;
                while (text[start + cur] != '\0')
                {
                        if (target[cur] == '\0')
                        {
                                return 1;
                        }
                        if (target[cur] == text[start + cur])
                        {
                                cur++;
                        }
                        else
                        {
                                start = start + cur - failure_array[cur];
                                cur = failure_array[cur];
                                if (cur < 0)
                                        cur = 0;
                        }
                }
                return target[cur] == '\0';
        }

        void initialise_array(char *target, int failure_array[], int n)
        {
                for (int i = 0; i < n; i++)
                {
                        failure_array[i] = 0;
                        for (int postfix_start = 1; postfix_start < i; postfix_start++)
                        {
                                int postfix_size = i - postfix_start;
                                int match = 1;
                                // Check if postfix matches the prefix
                                for (int prefix_i = 0; prefix_i < postfix_size; prefix_i++)
                                {
                                        if (target[prefix_i] != target[postfix_start + prefix_i])
                                        {
                                                match = 0;
                                        }
                                }
                                if (match)
                                {
                                        failure_array[i] = postfix_size;
                                        break;
                                }
                        }
                }
                failure_array[0] = -1;
        }

        int main(int argc, char *argv[])
        {
                char *target = "cart cars";
                int failure_array[9];
                initialise_array(target, failure_array, 9);
                for (int i = 0; i < 9; i++)
                {
                        printf("%d ", failure_array[i]);
                }
                printf("\n");
                char *text = "cars cart cars";
                printf("%d\n", kmp(text, target, failure_array));
        }