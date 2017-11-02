# Playman-Track-Field

Playman Track&amp;Field

Problem Description

田径运动会圆满的闭幕了，我们寝室的4名同学是我班最卖力的啦啦队员，每天都在看台上为班级里的运动员们加油助威，为我班获得精神文明奖立下了汗马功劳。可是遗憾的是，与我校的其他近2万名同学一样，我们自己不能上场表演 ：(于是，我们4名同学为下一届校运会发明了一种人人都能参加的比赛项目：

在地面上有N 个大小不等的长方形陷阱，每个陷阱的周长各不相同，每个参赛者都有一个沙包，闭上眼睛把它扔向地面，如果沙包掉到了某个陷阱里，那么这个参赛者根据这个陷阱的周长长度（如50米），绕跑道跑陷阱的周长长度（如50米），如果沙包没有掉到任何一个陷阱里，那么恭喜你，你跑0米。

有m<20000个同学参加了比赛，为了给跑步跑得最多的三位同学(冠军、亚军、季军)颁发安慰奖，必须给这m个同学的跑的长度按从多到少排序。
如下图一样的坐标系与长方形，这些长方形（陷阱）的四条边都与X轴或Y轴平行，它们之间互不相交，它们的左上角顶点的坐标与右下角顶点的坐标已知，给定一个你扔出去的沙包（看作是一个点）的坐标，可以得到你要跑的距离。（注意，这里的坐标值都不超过10000）

Input

第一行是两个正整数m<20000，n<100，它表示有m 个同学参加了扔沙包比赛，有n个陷阱。

接下去m行是m个同学扔出去的沙包的坐标，每一行都是两个正整数。

接下去的n行是陷阱的坐标，每行有4个正整数，它们从左到右分别是：陷阱左下角顶点的横坐标的值、陷阱左下角顶点的纵坐标的值，陷阱右上角顶点的横坐标的值、陷阱右上角顶点的纵坐标的值。

Output

m个同学按跑的距离的多少，从多到少输出，一个数字一行。

Sample Input

5 3 15 27 32 93 22 3 98 4 65 23 22 65 100 76 2 5 7 9 54 6 94 24

Sample Output

116 0 0 0 0

代码：

#include<cstdio>
  
#include<algorithm>
  
using namespace std;

typedef struct

{

    int x;
    
    int y;
    
    int len;
    
}PLAYER;

typedef struct

{

    int x1;
    
    int y1;
    
    int x2;
    
    int y2;
    
    int len;
    
}RECTANGLE;

void meters(PLAYER *p[],int m,RECTANGLE rec[],int n);

void mysort(PLAYER *p[],int m);

int main()

{
    PLAYER player[20000],*p[20000];
    
    
    RECTANGLE rec[100];
    
    int m,mi,n,ni;
    
    while(scanf("%d%d",&m,&n)!=EOF){
    
        for(mi=0;mi<m;mi++)
        
        {
        
            p[mi]=&player[mi];
            
            scanf("%d%d",&p[mi]->x,&p[mi]->y);
            
            p[mi]->len=0;
            
        }
        
        for(ni=0;ni<n;ni++)
        
        {
        
            scanf("%d%d%d%d",&rec[ni].x1,&rec[ni].y1,&rec[ni].x2,&rec[ni].y2);
            
            rec[ni].len=2*(rec[ni].y2-rec[ni].y1+rec[ni].x2-rec[ni].x1);
            
        }
        
        meters(p,m,rec,n);
        
        mysort(p,m);
        
        for(mi=0;mi<m;mi++)
        
            printf("%d\n",p[mi]->len);
            
    }
    
    return 0;
    
}

void meters(PLAYER *p[],int m,RECTANGLE rec[],int n)

{

    int ni,mi;
    
    for(mi=0;mi<m;mi++)
    
        for(ni=0;ni<n;ni++)
        
            if(p[mi]->x>=rec[ni].x1&&p[mi]->x<=rec[ni].x2&&p[mi]->y>=rec[ni].y1&&p[mi]->y<=rec[ni].y2)
            
            {
            
                p[mi]->len+=rec[ni].len;
                
                
                break;
                
            }
}

void mysort(PLAYER *p[],int m)

{

    int i,j,k;
    
    PLAYER *t;
    
    for(i=0;i<m-1;i++)
    
    {
    
        k=i;
        
        for(j=i+1;j<m;j++)
        
            if(p[k]->len<p[j]->len) k=j;
            
        t=p[i];p[i]=p[k];p[k]=t;
        
    }
    
}
