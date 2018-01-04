Tags: 时间序列篇

*ARMA模型* 
=====================

##定义

把具有如下结构的模型称为自回归移动平均模型，简记为$ARMA(p,q)$：$$\begin{cases} x_t = \phi_0 + \phi_1 x_{t-1} + \cdots + \phi_p x_{t-p} + \epsilon_t - \theta_1 \epsilon_{t-1} - \cdots - \theta_q \epsilon_{t-q} \\\\ \phi_p \neq 0, \theta_q \neq 0 \\\\ E(\epsilon_t) = 0, Var(\epsilon_t) = \sigma_{\epsilon}^2, E(\epsilon_t \epsilon_s) = 0, s \neq t \\\\ E(x_t \epsilon_s) = 0, \forall s < t \end{cases}$$若 $\phi_0 = 0$，该模型称为中心化$ARMA(p,q)$模型.

引进延迟算子，$ARMA(p,q)$模型简记为:$$\Phi(B) x_t = \Theta(B) \epsilon_t $$式中:

- $\Phi(B) = 1 - \phi_1 B - \cdots - \phi_p B^p $，为$p$阶自回归系数多项式.

- $\Theta(B) = 1 - \theta_1 B - \cdots - \theta_q B^q$， 为$q$阶移动平均系数多项式.

显然：

- 当$q = 0$时，$ARMA(p,q)$模型就退化成了 $AR(p)$模型.

- 当 $p = 0$ 时，$ARMA(p,q)$模型就退化成了 $MA(q)$模型.

所以，$AR(p)$模型和 $MA(q)$模型实际上是 $ARMA(p,q)$模型的特例，它们都统称为 $ARMA$模型.而 $ARMA(p,q)$模型的统计性质也正是 $AR(p)$模型和 $MA(q)$模型统计性质的有机组合.

______________________________________________

##平稳条件和可逆条件

对于一个 $ARMA(p,q)$模型，令 $z_t = \Theta(B) \epsilon_t$ ，显然 $\{z_t\}$是一个均值为零、方差为 $(1+\theta_1^2 + \cdots + \theta_q^2) \sigma_{\epsilon}^2$ 的平稳序列.于是 $ARMA(p,q)$模型可以改写为如下形式：$$\Phi(B) x_t = z_t$$类似于$AR(p)$模型平稳性的分析，容易推导出 $ARMA(p,q)$模型的平稳条件是: $\Phi(B) = 0$ 的根都在单位圆外.也就是说，$ARMA(p,q)$模型的平稳性完全由其自回归部分的平稳性决定.

同理，可以推导出 $ARMA(p,q)$模型的可逆条件和 $MA(q)$模型的可逆条件完全相同: 当 $\Theta(B) = 0$ 的根都在单位圆外时，$ARMA(p,q)$模型可逆.

当 $\Phi(B) = 0, \Theta(B) = 0$ 的根都在单位圆外时，$ARMA(p,q)$模型称为平稳可逆模型，这是一个由它的自相关系数唯一识别的模型.

_____________________________________________

##传递形式与逆转形式

对于一个平稳可逆 $ARMA(p,q)$模型，它的传递形式为:$$x_t = \Phi^{-1}(B) \Theta(B) \epsilon_t = \sum_{j=0}^{\infty}{G_j \epsilon_{t-j}}$$式中，$\{G_0, G_1, G_2, \cdots \}$ 为 $Green$函数.

通过待定系数法，容易得到 $ARMA(p,q)$模型场合下 $Green$函数的递推公式为:$$G_0 = 1 \\\\ G_k = \sum_{j=1}^k{\phi_j' G_{k-j} - \theta_k'}, k \geq 1$$式中:$$\phi_j' = \begin{cases} \phi_j , 1 \leq j \leq p \\ 0 , j > p \end{cases} , \theta_k' = \begin{cases} \theta_k , 1 \leq k \leq q \\ 0 , k > q \end{cases}$$同理，可以得到 $ARMA(p,q)$模型的逆转形式为:$$\epsilon_t = \Theta^{-1}(B) \Phi(B) x_t = \sum_{j=0}^{\infty}{I_j x_{t-j}}$$式中，$\{I_1, I_1, \cdots\}$为逆函数.

通过待定系数法容易得到逆函数的递推公式:$$\begin{cases} I_0 = 1 \\ I_k = \sum_{j=1}^k {\theta_j' I_{k-j} - \phi_k'} , k \geq 1 \end{cases}$$式中，$\theta_k' 和 \phi_k'$的定义同上.

__________________________________________

##$ARMA(p,q)$模型的统计性质

###均值

对于一个非中心化平稳可逆的 $ARMA(p,q)$模型$$x_t = \phi_0 + \phi_1 x_{t-1} + \phi_2 x_{t-2} + \cdots + \phi_p x_{t-p} + \epsilon_t - \theta_1 \epsilon_{t-1} - \theta_2 \epsilon_{t-2} - \cdots - \theta_q \epsilon_{t-q}$$两边同求均值，有$$E(x_t) = \frac{\phi_0}{1 - \phi_1 - \cdots - \phi_p}$$

_____________________________________________

###自协方差函数

$$\gamma(k) = E(x_t x_{t+k}) \\ = E\left[ \left( \sum_{i=0}^{\infty}{G_i \epsilon_{t-i}} \right) \left( \sum_{j=0}^{\infty}{G_j \epsilon_{t+k-j}} \right) \right] \\ E \left[ \sum_{i=0}^{\infty} {G_i} \sum_{j=0}^{\infty}{G_j \epsilon_{t-i} \epsilon_{t+k-j}} \right] \\ = \sigma_{\epsilon}^2 \sum_{i=0}^{\infty}{G_i G_{i+k}}$$

___________________________________________

###自相关系数

$$\rho(k) = \frac{\gamma(k)}{\gamma(0)} = \frac{\sum_{j=0}^{\infty}{G_j G_{j+k}}}{\sum_{j=0}^{\infty}{G_j^2}}$$根据自相关系数的表达式很容易判断 $ARMA(p,q)$模型的自相关系数不截尾.这和 $ARMA(p,q)$模型可以转换为无穷阶移动平均模型的性质是一致的.同理，根据 $ARMA(p,q)$模型可以转化为无穷阶自回归模型，可以判断它的偏自相关系数也不截尾.

___________________________________________

##R程序演示

