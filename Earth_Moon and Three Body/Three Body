function [] = threebody()
G = 6.67*10^(-11);
pos_p1 = [rand,rand,rand]*10^7;
pos_p2 = [rand,rand,rand]*10^7;
pos_p3 = [rand,rand,rand]*10^7;

m_p1 = rand()*10^23;
m_p2 = rand()*10^23;
m_p3 = rand()*10^23;

v_p1 = [rand,rand,rand]*10^3;
v_p2 = [rand,rand,rand]*10^3;
v_p3 = [rand,rand,rand]*10^3;

dt = 1;
flag = 0;  

figure
grid on
view(3)
title('三体模型')
colordef black
axis equal
xlabel('x(m)')
ylabel('y(m)')
zlabel('z(m)')
hold on

p1 = plot3(pos_p1(1),pos_p1(2),pos_p1(3),'r:.','markersize',20);
p2 = plot3(pos_p2(1),pos_p2(2),pos_p2(3),'b:.','markersize',20);
p3 = plot3(pos_p3(1),pos_p3(2),pos_p3(3),'w:.','markersize',20);
h1 = animatedline('color','r');
h2 = animatedline('color','b');
h3 = animatedline('color','w');

[A,map] = rgb2ind(frame2im(getframe(gcf)),256);
imwrite(A,map,'1.gif','LoopCount',65535,'DelayTime',0.01);
while true
    r_12 = normest(pos_p1-pos_p2);
    r_13 = normest(pos_p1-pos_p3);
    r_23 = normest(pos_p2-pos_p3);
    F_12 = G*m_p1*m_p2/(r_12^2);
    F_13 = G*m_p3*m_p1/(r_13^2);
    F_23 = G*m_p3*m_p2/(r_23^2);
    n_12 = (pos_p1-pos_p2)/normest(pos_p1-pos_p2);
    n_13 = (pos_p1-pos_p3)/normest(pos_p1-pos_p3);
    n_23 = (pos_p2-pos_p3)/normest(pos_p2-pos_p3);
    a_1 = (-F_12*n_12-F_13*n_13)/m_p1;
    a_2 = (F_12*n_12-F_23*n_23)/m_p2;
    a_3 = (F_13*n_13+F_23*n_23)/m_p3;
    pos_p1 = pos_p1+v_p1*dt+0.5*a_1*dt^2;
    pos_p2 = pos_p2+v_p2*dt+0.5*a_2*dt^2;
    pos_p3 = pos_p3+v_p3*dt+0.5*a_3*dt^2;
    v_p1 = v_p1+a_1*dt;
    v_p2 = v_p2+a_2*dt;
    v_p3 = v_p3+a_3*dt;
    flag = flag+1;
    if flag == 500
        set(p1,'Xdata',pos_p1(1),'Ydata',pos_p1(2),'Zdata',pos_p1(3));
        set(p2,'Xdata',pos_p2(1),'Ydata',pos_p2(2),'Zdata',pos_p2(3));
        set(p3,'Xdata',pos_p3(1),'Ydata',pos_p3(2),'Zdata',pos_p3(3));
        addpoints(h1,pos_p1(1),pos_p1(2),pos_p1(3));
        addpoints(h2,pos_p2(1),pos_p2(2),pos_p2(3));
        addpoints(h3,pos_p3(1),pos_p3(2),pos_p3(3));
        hold on 
        drawnow update
        [A,map] = rgb2ind(frame2im(getframe(gcf)),256);
        imwrite(A,map,'1.gif','WriteMode','append','DelayTime',0.01);
        flag = 0;      
    end
if abs(r_12) < 10^5 || abs(r_13) < 10^5 || abs(r_23) < 10^5
    break
end

end
