#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/types.h>
#include<sys/wait.h>

int main(void)
{
        int fd[2],nbytes;
        pid_t childpid, wpid;
        int users = 95;
        char mystring[80];
        char readbuffer[80];
        int arr[10] = {5,7,9,2,6,3,4,1,7,9};
        int i =0;
        int n =0;
        int status =0;
        int sum =0;

        pipe(fd);
        if((childpid = fork()) == -1)
        {
                perror("fork");
                exit(1);

        }

        if(childpid != 0)
        {

                //Parent Closes read side of pipe
                close(fd[0]);

                //Convert integer array into a string using sprintf function
                for(int i =0; i<10; i++)
                        n+= sprintf(&mystring[n], "%d" , arr[i]);


                //Add NULL character to mystring
                mystring[(sizeof(arr)/4)] = '\0';

                //Send string of integer values to child from parent
                write(fd[1], mystring, sizeof(mystring));



                //Waiting for child to terminate
                wpid = wait(&status);
                if(wpid != -1)
                {
                        printf("Parent printing wait id: ");
                        printf("%d", wpid);
                        printf("\n");

                }

        }

        else
        {
                //child closes output side of pipe
                close(fd[1]);

                //child reads in the string the parent sent
                read(fd[0], mystring, sizeof(mystring));

                //Summing values in the array

                int i =0;
                while(mystring[i] != '\0')
                {
                        sum += mystring[i] - '0';
                        ++i;
                }


                printf("The sum of the integers is: ");
                printf("%d", sum);
                printf("\n");
                //Close input side of pipe
                close(fd[0]);

                exit(0);


        }


        return 0;

}
