---
title: MATLAB蚁群算法 
categories:  
- 杂项 
tags:
- matlab
- 算法
---

## MATLAB蚁群算法

#### 之前做的一个作业，想复习MATLAB语法的话可以看看

- 算法（tsp_ant.m）
```matlab
function tsp_ant(inputx,inputy)
    tic;
%   inputx和inputy都是一维列向量，分别代表城市的x横坐标和纵坐标
    C = [inputx,inputy]; %记录了城市的坐标
    times_limit = 500; %最大迭代次数
    m = 20; %蚂蚁数量
    n = size(inputx,1); %城市数量，n为inputx第一维的长度
    graph = zeros(n,n); %存储距离
    alpha = 1; %信息素的加权值
    beta = 3; %能见度的加权值
    ro = 0.1; %信息素蒸发系数%每次使用前更新
    Q = 10^6; %信息素增加强度系数
    best_route = zeros(times_limit,n); %每次迭代的最佳路线
    best_length = inf * ones(times_limit,1); %每次迭代的最佳路线的长度
    
%   Step1 : 变量初始化
    for i = 1:n
        for j = 1:n
            if(i ~= j)
                graph(i,j) = ((C(i,1) - C(j,1))^2 + (C(i,2) - C(j,2))^2)^0.5; 
            else
                graph(i,j) = realmin; 
            end
        end
    end
    iota = 1./graph; 
    tau = ones(n,n); 
    tabu = zeros(m,n);  
    average_length = zeros(times_limit,1); 
    
%   Step2 : 放置蚂蚁
    for time = 1:times_limit 
        location = randi(n,1,m);
        tabu(:,1) = (location(1:m))'; 
        
%   Step3 : 蚂蚁完成各自路径
        for j = 2:n 
            for i = 1:m
                visited = tabu(i,1:(j-1)); 
                next_cities = zeros(1,(n-j+1)); 
                next_properties = zeros(1,(n-j+1)); 
                index = 1; 
                for k = 1:n
                    if ismember(k,visited) == 0 
                        next_cities(index) = k;
                        index = index + 1;
                    end
                end
                for k = 1:length(next_cities) 
                    next_properties(k) = (tau(visited(end),next_cities(k))^alpha) * (iota(visited(end),next_cities(k))^beta);
                end
                next_properties = next_properties/sum(next_properties);
                %使用轮盘赌的方法模拟按概率选择下一城市的过程
                roulette = cumsum(next_properties);
                pointer = rand;
                for k = 1:length(roulette)
                    if roulette(k) >= pointer
                        break
                    end
                end
                to_visit = next_cities(k);
                tabu(i,j) = to_visit; 
            end
        end
        if time >= 2
            tabu(1,:) = best_route(time-1,:); 
        end
        
%   Step4 : 记录本次迭代最佳路线
        route_length = zeros(m,1); 
        for i = 1:m
            route_i = tabu(i,:); 
            for j = 1:(n-1)
                route_length(i) = route_length(i) + graph(route_i(j),route_i(j+1));
            end
            route_length(i) = route_length(i) + graph(route_i(1),route_i(n)); 
        end
        best_length(time) = min(route_length); 
        [~,loc] = min(route_length);
        best_route(time,:) = tabu(loc,:); 
        average_length(time) = mean(route_length); 
        
%   Step5 : 更新信息素
        delta_tau = zeros(n,n);
        for i = 1:m
            for j = 1:(n-1) 
                delta_tau(tabu(i,j),tabu(i,j+1)) = delta_tau(tabu(i,j),tabu(i,j+1)) + Q/route_length(i); 
            end
            delta_tau(tabu(i,n),tabu(i,1)) = delta_tau(tabu(i,n),tabu(i,1)) + Q/route_length(i);
        end
        tau = (1-ro)*tau + delta_tau; 
        
%   Step6 : 路径表格清零
        tabu = zeros(m,n);
    end
    
    toc;
%   Step7 : 绘制图形
    [~,loc] = min(best_length); 
    the_route = best_route(loc,:); 
    the_length = best_length(loc); 
    %绘制图1
    figure(1)
    set(gcf,'unit','centimeters','position',[5,5,20,20]);
    axis square;
    scatter(C(:,1),C(:,2)); %绘制散点图
    hold on
    for i = 1:n-1
        plot([C(the_route(i),1),C(the_route(i+1),1)],[C(the_route(i),2),C(the_route(i+1),2)],'-rd','LineWidth',3,'MarkerEdgeColor','k','MarkerFaceColor','b'); 
        hold on
    end
    plot([C(the_route(1),1),C(the_route(n),1)],[C(the_route(1),2),C(the_route(n),2)],'-rd','LineWidth',3,'MarkerEdgeColor','k','MarkerFaceColor','b');
    hold on
    xlabel('x');
    ylabel('y');
    title('最短路线图');
    text(72,99,['最短路径长度 = ',num2str(the_length)]);
    text(72,96,['历史平均长度 = ',num2str(mean(average_length))]);
end
```

- 应用（控制台）

```matlab
>> x = round(rand(1,100)*100)'
>> y = round(rand(1,100)*100)'
>> tsp_ant(x,y)
```

