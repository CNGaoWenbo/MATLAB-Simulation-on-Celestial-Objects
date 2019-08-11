function [] = earth_moon()
%两个选项，默认是输出地月绕日公转的GIF图。调整几行程序输出地月公转时的追踪视角
%Two options are avilable. Program will export a GIF picturing the Earth
%and the Moon revolution around the Sun. Adjust few lines to demonstrate
%how the Moon revovles around the Earth.
G = 6.67*10^(-11);
%rel = 5*10^8; %地月追踪视角开启此行 Activate this Line when Tracking the "Earth-Moon" 
%初始位置、质量、速度设置 Postion, Mass and Velocity
pos_sun = [0,0];
pos_earth = [1.5*10^11,0];
pos_moon = [pos_earth(1)+3.84*10^8,2];
m_sun = 1.989*10^30;
m_earth = 5.965*10^24;
m_moon = 7.349*10^22;
v_earth = [0,2.9783*10^4];
v_moon = [0,v_earth(2)+1.0273*10^3];
%--%
dt = 100;
flag = 0;   
%画图模块 Plot
figure
title('地月模型 Simplified Earth-Moon System')
colordef black
axis equal
xlabel('x(m)')
ylabel('y(m)')
hold on
%绘制天体位置 Plot Postion of Celestial Bodies
earth = plot(pos_earth(1),pos_earth(2),'b:.','markersize',20);
sun  = plot(pos_sun(1),pos_sun(2),'r:.','markersize',60); %地月追踪视角取消此行 Deactivate this Line when Tracking the "Earth-Moon"
moon = plot(pos_moon(1),pos_moon(2),'w:.','markersize',5);
%动态线条 Animated Lines
h1 = animatedline('color','b');
h2 = animatedline('color','r'); %地月追踪视角取消此行 Deactivate this Line when Tracking the "Earth-Moon"
h3 = animatedline('color','w');
%GIF图输出 Export a Figure in GIF
[A,map] = rgb2ind(frame2im(getframe(gcf)),256);
imwrite(A,map,'1.gif','LoopCount',65535,'DelayTime',0.01);
while true
    %天体间距离 Distance between two objects
    r_se = normest(pos_earth-pos_sun);%se: sun-earth
    r_sm = normest(pos_sun-pos_moon);%sm: sun-moon
    r_em = normest(pos_earth-pos_moon);%em: earth-moon
    %万有引力数值 Value of Universal Gravitation
    F_se = G*m_sun*m_earth/(r_se^2);
    F_em = G*m_moon*m_earth/(r_em^2);
    F_sm = G*m_moon*m_sun/(r_sm^2);
    %万有引力方向 Direction of Universal Gravitation
    n_se = (pos_sun-pos_earth)/normest(pos_sun-pos_earth);
    n_sm = (pos_sun-pos_moon)/normest(pos_sun-pos_moon);
    n_em = (pos_earth-pos_moon)/normest(pos_earth-pos_moon);
    %加速度 Acceleration 
        %note: Ignore the Acceleration of the Sun
    a_earth = (F_se*n_se-F_em*n_em)/m_earth;
    a_moon = (F_sm*n_sm+F_em*n_em)/m_moon;
    %更新天体坐标 Updated Postion
    pos_earth = pos_earth+v_earth*dt+0.5*a_earth*dt^2;
    pos_moon = pos_moon+v_moon*dt+0.5*a_moon*dt^2;
    %更新天体速度 Update Velocity
    v_earth = v_earth+a_earth*dt;
    v_moon = v_moon+a_moon*dt;
    flag = flag+1;%计数 counting
    if flag == 500 %每计算500点插入图像 Add 1 Point per 500 Caculations
        set(earth,'Xdata',pos_earth(1),'Ydata',pos_earth(2));
        set(sun,'Xdata',pos_sun(1),'Ydata',pos_sun(2)); %地月追踪视角取消此行 Deactivate this Line when Tracking the "Earth-Moon"
        set(moon,'Xdata',pos_moon(1),'Ydata',pos_moon(2));
        addpoints(h1,pos_earth(1),pos_earth(2));
        addpoints(h2,pos_sun(1),pos_sun(2)); %地月追踪视角取消此行 Deactivate this Line when Tracking the "Earth-Moon"
        addpoints(h3,pos_moon(1),pos_moon(2));
        hold on 
        %axis([pos_earth(1)-5*rel,pos_earth(1)+10*rel,pos_earth(2)-10*rel,pos_earth(2)+rel %地月追踪视角开启此行 Activate this Line when Tracking the "Earth-Moon" 
        drawnow update
        [A,map] = rgb2ind(frame2im(getframe(gcf)),256);
        imwrite(A,map,'1.gif','WriteMode','append','DelayTime',0.01);
        flag = 0;
   end
if abs(r_se) <= 1.35*10^7 %地月间距小于洛希极限终止 in case distance between Earth and Moon is smaller than the Roche's limit
    break
end

end
