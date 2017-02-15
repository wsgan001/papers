# Abstract
This paper first introduces the key features of big data in different processing modes and their typical application scenarios,
as well as corresponding representative processing systems. It then summarizes three development trends of big data processing systems.
Next, the paper gives a brief survey on system supported analytic technologies and applications (including deep learning, knowledge
computing, social computing, and visualization), and summarizes the key roles of individual technologies in big data analysis and
understanding. Finally, the paper lays out three grand challenges of big data processing and analysis, i.e., data complexity, computation
complexity, and system complexity. Potential ways for dealing with each complexity are also discussed.  
**Key words**: dig data; data analysis; deep learning; knowledge computing; social computing; visualization

　　近几年,大数据迅速发展成为科技界和企业界甚至世界各国政府关注的热点.《Nature》和《Science》等相
继出版专刊专门探讨大数据带来的机遇和挑战.著名管理咨询公司麦肯锡称:“数据已经渗透到当今每一个行业
和业务职能领域,成为重要的生产因素.人们对于大数据的挖掘和运用,预示着新一波生产力增长和消费盈余浪
潮的到来”[1].美国政府认为大数据是“未来的新石油”,一个国家拥有数据的规模和运用数据的能力将成为综合
国力的重要组成部分,对数据的占有和控制将成为国家间和企业间新的争夺焦点.大数据已成为社会各界关注
的新焦点,“大数据时代”已然来临.  
　　什么是大数据,迄今并没有公认的定义.从宏观世界角度来讲,大数据是融合物理世界(physical world)、信息
空间和人类社会(human society)三元世界的纽带,因为物理世界通过互联网、物联网等技术有了在信息空间(cyberspace)中的大数据反映,而人类社会则借助人机界面、脑机界面、移动互联等手段在信息空间中产生自己
的大数据映像[2,3].从信息产业角度来讲,大数据还是新一代信息技术产业的强劲推动力.所谓新一代信息技术
产业本质上是构建在第三代平台上的信息产业,主要是指大数据、云计算、移动互联网(社交网络)等.IDC 预测,
到2020 年第三代信息技术平台的市场规模将达到5.3 万亿美元,而从2013 年~2020 年,IT 产业90%的增长将由
第三代信息技术平台驱动.从社会经济角度来讲,大数据是第二经济(second economy[4])的核心内涵和关键支撑.
第二经济的概念是由美国经济学家Auther 在2011 年提出的.他指出由处理器、链接器、传感器、执行器以及
运行在其上的经济活动形成了人们熟知的物理经济(第一经济)之外的第二经济(不是虚拟经济).第二经济的本
质是为第一经济附着一个“神经层”,使国民经济活动能够变得智能化,这是100 年前电气化以来最大的变化.
Auther 还估算了第二经济的规模,他认为到2030 年,第二经济的规模将逼近第一经济.而第二经济的主要支撑是
大数据,因为大数据是永不枯竭并不断丰富的资源产业.借助于大数据,未来第二经济下的竞争将不再是劳动生
产率而是知识生产率的竞争.  
　　相较于传统的数据,人们将大数据的特征总结为5 个V,即体量大(volume)、速度快(velocity)、模态多
(variety)、难辨识(veracity)和价值大密度低(value).但大数据的主要难点并不在于数据量大,因为通过对计算机
系统的扩展可以在一定程度上缓解数据量大带来的挑战.其实,大数据真正难以对付的挑战来自于数据类型多
样(variety)、要求及时响应(velocity)和数据的不确定性(veracity).因为数据类型多样使得一个应用往往既要处
理结构化数据,同时还要处理文本、视频、语音等非结构化数据,这对现有数据库系统来说难以应付;在快速响
应方面,在许多应用中时间就是利益.在不确定性方面,数据真伪难辨是大数据应用的最大挑战.追求高数据质
量是对大数据的一项重要要求,最好的数据清理方法也难以消除某些数据固有的不可预测性.  
　　为了应对大数据带来的上述困难和挑战,以Google,Facebook,Linkedin,Microsoft 等为代表的互联网企业近
几年推出了各种不同类型的大数据处理系统.借助于新型的处理系统,深度学习、知识计算、可视化等大数据
分析技术也得已迅速发展,已逐渐被广泛应用于不同的行业和领域.本文从系统支撑下的大数据分析角度入手,
介绍了不同的大数据处理模式与代表性的处理系统,并对深度学习、知识计算等重要的大数据分析技术进行综
述,最后指出大数据处理和分析所面临的3 个核心挑战,并提出可能的解决思路.