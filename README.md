# Graphical Method

clc
clear all

A=[-1 3; 1 1; 1 -1];
B=[10; 6; 2];


x1=0:1:max(B);


x11=(B(1)-A(1,1).*x1)./A(1,2);
x21=(B(2)-A(2,1).*x1)./A(2,2);
x31=(B(3)-A(3,1).*x1)./A(3,2);


x11=max(0,x11);
x21=max(0,x21);
x31=max(0,x31);


plot(x1,x11,'r',x1,x21,'b',x1,x31,'g')
title('x1 vs x2')
xlabel('value of x1')
ylabel('value of x2')
legend('-x1+3x2=10','x1+x2=6','x1-x2=2')
grid on

cx1=find(x1==0); 
c1=find(x11==0); 
Line1=[x1(:,[c1 cx1]); x11(:,[c1 cx1])]';

c2=find(x21==0); 
Line2=[x1(:,[c2 cx1]); x21(:,[c2 cx1])]';

c3=find(x31==0); 
Line3=[x1(:,[c3 cx1]); x31(:,[c3 cx1])]';

corpt=unique([Line1;Line2;Line3],'rows');


pt=[0;0];
for i=1:size(A,1)
    A1=A(i,:);
    B1=B(i,:);
    for j=i+1:size(A,1)
        A2=A(j,:);
        B2=B(j,:);
        A4=[A1;A2];
        B4=[B1;B2];
        X=A4\B4;
        pt=[pt X];
    end
end
ptt=pt';


allpt=[ptt;corpt];
points=unique(allpt,'rows');



x1=allpt(:,1);
x2=allpt(:,2);

cons1=-x1+3.*x2-10;
h1=find(cons1>0);
allpt(h1,:)=[];

x1=allpt(:,1);
x2=allpt(:,2);

cons2=x1+x2-6;
h2=find(cons2>0);
allpt(h2,:)=[];

x1=allpt(:,1);
x2=allpt(:,2);

cons3=x1-x2-2;
h3=find(cons3>0);
allpt(h3,:)=[];

point=allpt;


P=unique(point,'rows');


c=[1 5];

for i=1:size(P,1)
    fn(i,:)=(sum(P(i,:).*c));
end

ver_fns=[P fn];



[Optval optposition]=max(fn);

Optval=ver_fns(optposition,:);

OPTIMAL_BFS=array2table(Optval)
