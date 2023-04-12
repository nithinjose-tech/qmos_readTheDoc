Sequence to Sequence Model
++++++++++++++++++++++++++

*Importing pandas package*::
    

        import pandas as pd






::
     
        df=pd.read_csv('/content/drive/MyDrive/Input Files/SW.csv')

*Installing simple transformers model*
::

     !pip install simpletransformers

*Frome simple trsanformers import the required sequence to sequence model*
::

     import logging
     import pandas as pd
     from simpletransformers.seq2seq import Seq2SeqModel, Seq2SeqArgs

::

        model_args = Seq2SeqArgs()
        model_args.num_train_epochs = 10
        model_args.no_save = True
        model_args.evaluate_generated_text = True
        model_args.evaluate_during_training = True
        model_args.evaluate_during_training_verbose = True
        model_args.min_length=130
        model_args.max_length=150


        model = Seq2SeqModel(
            encoder_decoder_type="bart",
            encoder_decoder_name="facebook/bart-large",
            args=model_args,
            use_cuda=False,
        )


*In the above code section we setting the parameters for the model.Set the min_length and max_length as per the requirement.Here the bart encoder-decoder introduced by Facebook is used*

::

     training_data=[]
     
        for i in range(0,40):
        df.iloc[i][1] = "\"" + df.iloc[i][1] + "\""
        df.iloc[i][2] = "\"" + df.iloc[i][2] + "\""
        training_data.append([df.iloc[i][1],df.iloc[i][2]])
        
::

    train_df = pd.DataFrame(
    training_data, columns=["input_text", "target_text"]
   )

::



       eval_data =[]

        for i in range(41,50):
        df.iloc[i][1] = "\"" + df.iloc[i][1] + "\""
        df.iloc[i][2] = "\"" + df.iloc[i][2] + "\""
        eval_data.append([df.iloc[i][1],df.iloc[i][2]])

::

      eval_df = pd.DataFrame(eval_data, columns=["input_text", "target_text"])

*Training the model with training documents and corresponging summary*

::

      model.train_model(train_df, eval_data=eval_df)

::

      results = model.eval_model(eval_df)

*Model predicting the summary of the sample document given*

::

      print(model.predict(
        [
           "Parliament convened Thursday vote whether move no-confidence motion that could bring government organized crime scandal. Thursday's vote put motion agenda will be indication government's chances survival, which are said be extremely slim. If approved, legislature will debate motions Monday and hold no-confidence vote Wednesday. The opposition accuses Prime Minister Mesut Yilmaz having ties organized crime and tampering privatization state bank. He denies charges. Ousting government power will open way struggle gangs, said Lutfu Esengun, deputy Islamic Virtue Party, which presented one three no-confidence motions Parliament. On Wednesday, 6th graf pvs After failing bring together political rivals coalition, Premier-designate Bulent Ecevit announced Saturday that he was returning his mandate Turkish president. In statement reported Anatolia news agency, Ecevit said he would see President Suleyman Demirel Monday morning. Ecevit, veteran leftist, was called form cabinet two weeks ago Mesut Yilmaz' coalition government collapsed no-confidence vote Parliament. Deputies accused Yilmaz, who has been serving acting premier, entertaining ties mob and tampering sale state bank. Refusing any alliance pro-Islamic Virtue Party, Turkey's largest party Parliament, Ecevit was unable create political alliance strong enough survive confidence vote deeply divided legislature. Ecevit tried vain form coalition government two rival center-right wing parties -- one led Yilmaz, other former Prime Minister Tansu Ciller. Ecevut's alternate efforts make minority coalition backing his Democratic Left Party Parliament also failed. Demirel will now have either ask someone else try form government or wait Jan. 10, when constitution allows him appoint caretaker cabinet lead country parliamentary elections, now scheduled April. Such cabinet would not have face confidence vote. Or Demirel could choose leave current caretaker government, headed Yilmaz, power elections. Bulent Ecevit, who was asked form new government Wednesday, is former prime minister best remembered ordering invasion Cyprus 1974 that made him overnight hero home. The invasion, short-lived coup supporters union Greece, has led division island. Throughout years, Ecevit, 73, has remained strong defender cause Turkish Cypriots As long Turkey lives, we won't allow oppression and subordination Turkish Cypriots hands Greek Cypriots, he said July 1997 23rd anniversary celebrations invasion. Ecevit, who was prime minister three times 1974, has years shed some socialist idealism he was known 70s. During his tenure deputy prime minister 17-month government that was toppled last week corruption scandal, he gave his backing liberal policies center-right-led coalition. He said he was carrying out duty bring stable government and spare Turkey crisis - reference tensions previous Islamic-led government and secular military. Though never Marxist, Ecevit was his early years viewed suspicion big business espousing socialism based heavy government social benefits and strong role state sector economy. Recently, however, he has helped government keep good terms IMF, which ordered strict curb public spending, and approved number state sell-offs. Under his leadership 70's, ties United States were tense. He has also expressed concern U.S.-led multinational force based Turkey that monitors no-fly zone Kurdish-controlled northern Iraq. He argues it it is helping create Kurdish state. His frequent visits Iraq meet President Saddam Hussein have turn raised suspicion Washington. Despite short alliance Islamic party 1974, he is staunch defender Turkey's secular traditions and pushed crackdown Islamic radicalism. Ecevit was born Istanbul 1925, intellectual family and studied literature prestigious American-run high school. He has taken some courses Harvard University. A former journalist, he entered politics 1957, rising leadership Republican People's Party 1972, becoming prime minister 1974, briefly 1977 and again 1978-79. He was barred politics years that followed 1980 military coup. He was imprisoned three times carrying political activities ban, mainly his wife 51 years, Rahsan, who formed Democratic Left Party 1985 and led it democratic reform 1987 allowed Ecevit back politics. In corruption-tainted Turkish politics, he remains known leader cleanest slate. Not his alliance Yilmaz who was ousted alleged ties mob and rigging privatization bank, tarnished his image. The chances new, strictly secular government Turkey faded Wednesday when potential coalition partner insisted giving Islamic party share power. The military, self-appointed guardians Turkey's secular system, is adamantly opposed inclusion Islamic Virtue, largest party parliament. Premier-designate Bulent Ecevit needs Turkey's two-center right parties hammer together secular coalition, Tansu Ciller, ex-premier who commands 99 votes parliament, rebuffed him Wednesday. Ecevit already has support her arch-rival, outgoing Premier Mesut Yilmaz, head other center-right party. But Mrs. Ciller said Wednesday she would not join forces Yilmaz, whose government collapsed Nov. 25 mafia scandal. Instead, she reiterated her demand government that would include Virtue. We do not oppose Mr. Ecevit's premiership. We will support him, only if all parties represented Parliament are included, Mrs. Ciller said. It was not clear what Ecevit's next move would be. He might try form fragile minority coalition. He might also admit defeat and return task forming government President Suleyman Demirel. Demirel could then choose any member parliament head government elections April. ANKARA, Turkey (AP) - Prime Minister Mesut Yilmaz Wednesday faced intense pressure step allegations that he interfered privatization contract and helped businessman linked mobster secure loans. Deniz Baykal, leader center-left Republican party whose backing parliament helps Yilmaz's minority government, said he would withdraw his support unless premier resigned immediately. Two opposition parties threatened press motion censure government. The allegations were made businessman Korkmaz Yigit, who claimed that Yilmaz and Gunes Taner, economy minister, had encouraged him buy state-run bank Turkbank, offering him loans other state banks ensure that his offer was highest bid. Yigit's allegations were carried Tuesday night two his TV channels which showed videotape he had made explain his version story his detention Monday evening questioning bidding. Yigit bought bank public auction August dlrs 600 million. The government suspended privatization last month lawmaker released audio tape conversation supposedly Yigit and mobster Alaattin Cakici. On that earlier tape, Cakici was heard assuring Yigit that he will fend rival bidders. It was not clear who made tape, which got hands opposition deputy. Yigit claimed Yilmaz and Taner were aware Cakici's involvement bidding bank urged him nevertheless go ahead bidding. Yilmaz has said that intelligence report revealing Yigit's ties Cakici only reached him Yigit won tender. Yigit said premier had also encouraged him buy mass-circulation national newspaper Milliyet, apparently ensure paper's backing his center-right Motherland party elections next year. Milliyet's sale Yigit was canceled scandal. Cakici was arrested France August. Turkey has requested his extradition. Last month State Minister Eyup Asik resigned allegations he had been close contact Cakici. Turkey's latest premier-designate got backing two key secular parties Monday his efforts form broad-based, coalition government, condition that his government stick Turkey's secular principles. The Islamic-oriented Virtue Party, however, withheld immediate support Yalim Erez. News reports said Virtue was holding out number Cabinet seats that reflected its standing largest party parliament. We are neither saying `yes' nor saying `no' this point, Virtue leader Recai Kutan said. Erez denied that two had discussed Cabinet posts. Erez, independent lawmaker, is trying form coalition government that would include Cabinet members several parties, including Virtue. The coalition would run country only parliamentary elections set April. Erez took efforts form government last week veteran leftist Bulent Ecevit gave up, unable convince Turkey's bickering center-left and center-right parties join him coalition that excluded Islamic-oriented party. Erez opened talks various party leaders Monday. He got support center-right leader Mesut Yilmaz, who said his party supported Erez long he had Ecevit's backing. As long our sensitivity secular, democratic regime is taken account, we will do our best help form new government and ensure it gets vote confidence, Ecevit said his talks Erez. Turkey's strongly secular military is opposed any deal that would bring Virtue power. It pressured Virtue's predecessor, Welfare Party, out power last year. Erez is supposed talk Tuesday center-right Tansu Ciller and Deniz Baykal, who leads center-left party. I am more and more optimistic every meeting, Erez told reporters meeting party leaders. Turkey has been trying form new government coalition government led Yilmaz collapsed last month allegations that he rigged sale bank. Yilmaz is now acting premier. A week Turkish government fell corruption scandal, President Suleyman Demirel Wednesday asked veteran left-wing politician known his personal honesty, Bulent Ecevit, form new government. Ecevit, who served prime minister three times 1970s, said he would immediately begin working fashion government that could command majority faction-ridden Parliament. He also suggested that although Parliament has set April 18 date new election, he might seek remain power longer period. It is wrong see this government simply election government, he said. There are problems that will not wait election. Military commanders, who hold ultimate power Turkey, have quietly told senior political figures, including Demirel, that they do not want quick election. They fear it will produce Parliament just divided present one, perhaps Islamic-oriented Virtue Party largest bloc. The commanders are also hoping exclude two country's leading politicians, outgoing Prime Minister Mesut Yilmaz and former Prime Minister Tansu Ciller, neither whom they trust, posts new government. Ecevit must now try build government that includes their center-right parties not them individuals. In meeting this week country's senior policy-making body, National Security Council, which military officers have strong say, set three priorities coming months. It said that government emerges forthcoming negotiations should dedicate itself fighting religious fundamentalism, Kurdish nationalism and criminal gangs that have infiltrated state apparatus. Among Ecevit's immediate challenges will be resolve political crisis Italy that broke out last month when Kurdish rebel leader Abdullah Ocalan was arrested Rome and then asked political asylum there. Turkey wants Ocalan sent here trial, Italy says it cannot extradite him long Turkey retains death penalty. Ecevit (pronounced EH-che-vit) is few senior Turkish politicians who favors abolition capital punishment. Together Demirel, Ecevit is cited Turks who complain continued dominance geriatric political elite here. He is 73 and has been politics most his adult life. Early his career Ecevit emerged spokesman Turkey's downtrodden masses. Perhaps more any other figure, he legitimized social democratic ideology climate where leftist sympathies were considered subversive. At same time, however, he has shown himself be fierce nationalist. He was prime minister when Turkey sent troops occupy northern Cyprus 1974 and is still considered hard-liner Cyprus. He is also uncompromising his opposition Kurdish nationalism. During his terms prime minister 1970s, Ecevit successfully undermined efforts move Turkey membership European Union, then called European Economic Community. He considered it instrument capitalist exploitation. Ecevit has also disturbed United States flirting anti-Western ideologies. In early 1990s, interval when he worked journalist, he traveled Iraq and wrote series articles favorable Saddam Hussein. He recently called better relations Turkey and Iraq, and maintains some anti-imperialist positions and suspicion capitalism that he developed 1960s. The Democratic Socialist Party, which Ecevit heads, is closely held family fiefdom. He and his wife carefully screen applicants membership and veto those whose personal loyalty Ecevit is suspect. During his terms prime minister '70s, Ecevit not appear be consensus builder, said Ilter Turan, professor political science Bilgi University Istanbul. It seems that nowadays he is more accommodating, so that perspective he may not be bad choice. On many issues that Turkish society is encountering now, he represents orientation which does not seem be totally tune times, Turan said. That would include his position issues privatization, integrating Turkey more fully international system, and devolution central authority. He has failed grasp where world is heading. He looks and analyzes world categories that are no longer useful or appropriate. Almost alone Turkish politicians, Ecevit lives modestly and has avoided any hint personal or financial scandal. He speaks fluent English, and his reading tastes run poetry and intellectual journals such The New York Review Books. He has translated works T.S. Eliot Turkish and published several volumes his poems. Opposition parties lodged no-confidence motions Wednesday Prime Minister Mesut Yilmaz allegations he interfered privatization bank and helped businessman linked mobster. Yilmaz' minority government could go if the small, center-left Republican Party, which gives him majority he needs parliament, votes him. The leader Republicans, Deniz Baykal, urged Yilmaz resign. But premier vowed Wednesday stay on, saying he was victim conspiracy. This is plot and it can't be reason resignation, Yilmaz said, adding that he intended continue struggle organized crime. Afterward, Baykal said Republicans would support no-confidence motion. The leader Democratic Turkey Party, Husamettin Cindoruk, said his party might withdraw governing coalition. He said party would announce its decision Thursday. The political turmoil sent Istanbul stock market plunging 14.9 percent. Premier-designate Bulent Ecevit said Thursday he would persist difficult task convincing key party leader join forces secular coalition. Ecevit, who was asked form new government Wednesday, desperately needs support 99 deputies ex-premier Tansu Ciller's center-right party. Ecevit, veteran leftist, already has support another center-right party led Mesut Yilmaz, whose government collapsed last week weight mafia scandal. Mrs. Ciller has not said if she would back Ecevit-led government and her long-standing rivalry Yilmaz makes Ecevit's job coalition-building difficult. I don't give that easily, neither do I lose hope that easily, Ecevit told his parliamentary group Thursday. Mrs. Ciller could lose grassroot support if she stands way new government, political columnist Ertugrul Ozkok wrote Thursday daily Hurriyet. This could put her odds her classic support base. Ecevit was expected meet Yilmaz Thursday, and other party leaders Friday. Turkey's secular parties are pressure join forces keep Islamic Virtue Party out power. Virtue is largest party Parliament, all-powerful military is fiercely opposed Islamic-led government. President Suleyman Demirel appeared likely turn some widely trusted lawmaker form Turkey's next government, veteran politician abandoned efforts Monday persuade bickering political leaders support him pro-secular coalition. Bulent Ecevit Democratic Left Party failed 3-week-old attempt form government that could command majority votes Parliament. It is now clear that no party leader can form government that can win vote confidence, former Premier Mesut Yilmaz said talks Demirel. We have told president that we will not hamper appointment deputy Parliament. With party leaders unable overcome differences, new premier-designate would most probably be affiliated party be trusted enough other parties follow independent line. Parliament Speaker Hikmet Cetin has been suggested likely candidate. The new appointment would be made days, Yilmaz told reporters. Demirel consulted Turkey's party leaders immediately Ecevit gave up. Most declared themselves favor government led lawmaker. Only center-right leader Tansu Ciller said she wanted government led party leader, and made clear she was willing take task. Turkey's parliament is split longstanding animosity its center-left and center-right parties. Yilmaz led last government, which collapsed November allegations he had ties organized crime and interfered sale state bank. By tradition, Demirel should then have asked leader Parliament's largest party form new government. But Demirel broke custom keep Islamic-oriented Virtue Party power. Turkey's staunchly secular military opposes return Islamic-led government. Modern Turkey has had only one Islamic-led government, formed 1995 elections, and military pressured it power failing stick country's secular traditions. Ecevit refused consult leader Virtue Party his efforts form government."
        ]
    )
  )

::

      results   

  

     


