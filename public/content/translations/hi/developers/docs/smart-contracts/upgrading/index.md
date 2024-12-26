---
title: स्मार्ट अनुबंधों को अपग्रेड करना
description: एथेरियम स्मार्ट अनुबंधों के लिए अपग्रेड पैटर्न का अवलोकन
lang: hi
---

एथेरियम पर स्मार्ट अनुबंध स्व-निष्पादन प्रोग्राम हैं जो एथेरियम वर्चुअल मशीन (EVM) में चलते हैं। ये प्रोग्राम डिज़ाइन द्वारा अपरिवर्तनीय हैं, जो अनुबंध परिनियोजित होने के बाद व्यावसायिक तर्क में किसी भी अपडेट को रोकते हैं।

जबकि अपरिवर्तनीयता अविश्वसनीयता, विकेंद्रीकरण और स्मार्ट अनुबंधों की सुरक्षा के लिए आवश्यक है, यह कुछ मामलों में एक कमी हो सकती है। उदाहरण के लिए, अपरिवर्तनीय कोड डेवलपर्स के लिए कमजोर अनुबंधों को ठीक करना असंभव बना सकता है।

हालांकि, स्मार्ट अनुबंधों में सुधार के लिए बढ़ते शोध ने कई अपग्रेड पैटर्न की शुरुआत की है। ये अपग्रेड पैटर्न डेवलपर्स को अलग-अलग अनुबंधों में व्यावसायिक तर्क रखकर स्मार्ट अनुबंधों (अपरिवर्तनीयता को संरक्षित करते हुए) को अपग्रेड करने में सक्षम बनाते हैं।

## आवश्यक शर्तें {#prerequisites}

आपको [स्मार्ट अनुबंध](/developers/docs/smart-contracts/), [स्मार्ट अनुबंध एनाटॉमी](/developers/docs/smart-contracts/anatomy/) और [एथेरियम वर्चुअल मशीन (EVM)](/developers/docs/evm/) की अच्छी समझ होनी चाहिए। यह मार्गदर्शिका यह भी मानती है कि पाठकों को प्रोग्रामिंग स्मार्ट अनुबंधों की समझ है।

## स्मार्ट अनुबंध अपग्रेड क्या है? {#what-is-a-smart-contract-upgrade}

एक स्मार्ट अनुबंध अपग्रेड में अनुबंध की स्थिति को संरक्षित करते हुए एक स्मार्ट अनुबंध के व्यावसायिक तर्क को बदलना शामिल है। यह स्पष्ट करना महत्वपूर्ण है कि अपग्रेडेबिलिटी और म्यूटेबिलिटी समान नहीं हैं, खासकर स्मार्ट अनुबंध के मामले में।

आप अभी भी एथेरियम नेटवर्क पर किसी पते पर परिनियोजित प्रोग्राम को नहीं बदल सकते। हालांकि, आप उस कोड को बदल सकते हैं जो निष्पादित होता है जब उपयोगकर्ता स्मार्ट अनुबंध के साथ इंटरैक्ट करते हैं।

यह निम्नलिखित तरीकों से किया जा सकता है:

1. एक स्मार्ट अनुबंध के कई संस्करण बनाना और पुराने अनुबंध से अनुबंध के एक नए उदाहरण में माइग्रेट करना (यानी, डेटा)।

2. व्यापार तर्क और राज्य को स्टोर करने के लिए अलग-अलग अनुबंध बनाना।

3. एक अपरिवर्तनीय प्रॉक्सी अनुबंध से एक परिवर्तनीय तर्क अनुबंध के लिए फ़ंक्शन कॉल को सौंपने के लिए प्रॉक्सी पैटर्न का उपयोग करना।

4. एक अपरिवर्तनीय मुख्य अनुबंध बनाना जो खास कामों को निष्पादित करने के लिए लचीले उपग्रह अनुबंधों के साथ इंटरफ़ेस करता है और निर्भर करता है।

5. प्रॉक्सी अनुबंध से तर्क अनुबंधों तक फ़ंक्शन कॉल को सौंपने के लिए हीरे के पैटर्न का उपयोग करना।

### अपग्रेड मैकेनिज़्म #1: कॉन्ट्रैक्ट माइग्रेशन {#contract-migration}

अनुबंध माइग्रेशन संस्करण पर आधारित है - एक ही सॉफ़्टवेयर के अद्वितीय राज्यों को बनाने और प्रबंधित करने का विचार। अनुबंध माइग्रेशन में मौजूदा स्मार्ट अनुबंध के एक नए उदाहरण को डिप्लॉय करना और नए अनुबंध में भंडारण और शेष राशि को स्थानांतरित करना शामिल है।

नए परिनियोजित अनुबंध में एक खाली भंडारण होगा, जिससे आप पुराने अनुबंध से डेटा पुनर्प्राप्त कर सकते हैं और इसे नए कार्यान्वयन में लिख सकते हैं। बाद में, आपको नए पते को दर्शाने के लिए पुराने अनुबंध के साथ सहभागिता करने वाले सभी अनुबंधों को अपडेट करना होगा।

अनुबंध माइग्रेशन में अंतिम चरण उपयोगकर्ताओं को नए अनुबंध का उपयोग करने के मकसद से स्विच करने के लिए राजी करना है। नया अनुबंध संस्करण उपयोगकर्ता शेष राशि और पते को बनाए रखेगा, जो अपरिवर्तनीयता को संरक्षित करता है। अगर यह टोकन-आधारित अनुबंध है, तो आपको पुराने अनुबंध को त्यागने और नए अनुबंध का उपयोग करने के लिए एक्सचेंज से भी संपर्क करना होगा।

अनुबंध माइग्रेशन उपयोगकर्ता इंटरैक्शन को तोड़े बिना स्मार्ट अनुबंधों को अपग्रेड करने के लिए एक अपेक्षाकृत सरल और सुरक्षित उपाय है। हालांकि, मैन्युअल रूप से उपयोगकर्ता भंडारण और शेष राशि को नए अनुबंध में स्थानांतरित करना समय-गहन है और उच्च गैस लागत उठा सकता है।

[अनुबंध प्रवास पर अधिक।](https://blog.trailofbits.com/2018/10/29/how-contract-migration-works/)

### अपग्रेड मैकेनिज़्म #2: डेटा को अलग करना {#data-separation}

स्मार्ट अनुबंधों को अपग्रेड करने का एक अन्य तरीका व्यापार तर्क और डेटा भंडारण को अलग-अलग अनुबंधों में अलग करना है। इसका मतलब है कि उपयोगकर्ता तर्क अनुबंध के साथ इंटरैक्ट करते हैं, जबकि डेटा स्टोरेज अनुबंध में संग्रहीत होता है।

तर्क अनुबंध में कोड निष्पादित होता है जब उपयोगकर्ता एप्लिकेशन के साथ इंटरैक्ट करते हैं। यह भंडारण अनुबंध का पता भी रखता है और डेटा प्राप्त करने और सेट करने के लिए इसके साथ इंटरैक्ट करता है।

इस बीच, भंडारण अनुबंध स्मार्ट अनुबंध से जुड़े स्टेट को रखता है, जैसे उपयोगकर्ता शेष राशि और पते। ध्यान दें कि भंडारण अनुबंध तर्क अनुबंध के स्वामित्व में है और इसे परिनियोजन पर बाद के पते के साथ कॉन्फ़िगर किया गया है। यह अनधिकृत अनुबंधों को संग्रहण अनुबंध को कॉल करने या उसके डेटा को अपडेट करने से रोकता है।

डिफ़ॉल्ट रूप से, संग्रहण अनुबंध अपरिवर्तनीय है—लेकिन आप उस तर्क अनुबंध को बदल सकते हैं जो इसे एक नए कार्यान्वयन के साथ इंगित करता है। इससे EVM में चलने वाले कोड में बदलाव हो जाएगा, जबकि स्टोरेज और बैलेंस बरकरार रहेगा।

इस अपग्रेड विधि का उपयोग करने के लिए संग्रहण अनुबंध में तर्क अनुबंध के पते को अद्यतन करने की आवश्यकता होती है। आपको पहले बताए गए कारणों के लिए संग्रहण अनुबंध के पते के साथ नए तर्क अनुबंध को भी कॉन्फ़िगर करना होगा।

अनुबंध माइग्रेशन की तुलना में डेटा को अलग करने का पैटर्न यकीनन लागू करना आसान है। हालांकि, आपको स्मार्ट अनुबंधों को दुर्भावनापूर्ण अपग्रेड करने से बचाने के लिए कई अनुबंधों का प्रबंधन करना होगा और जटिल प्राधिकरण योजनाओं को लागू करना होगा।

### अपग्रेड मैकेनिज़्म #3: प्रॉक्सी पैटर्न {#proxy-patterns}

प्रॉक्सी पैटर्न व्यापार तर्क और डेटा को अलग-अलग अनुबंधों में रखने के लिए डेटा को अलग करने की प्रक्रिया का भी उपयोग करता है। हालांकि, एक प्रॉक्सी पैटर्न में, भंडारण अनुबंध (जिसे प्रॉक्सी कहा जाता है) कोड निष्पादन के दौरान तर्क अनुबंध को कॉल करता है। यह डेटा को अलग करने के तरीके का एक रिवर्स है, जहां तर्क अनुबंध भंडारण अनुबंध को कॉल करता है।

प्रॉक्सी पैटर्न में यही होता है:

1. उपयोगकर्ता प्रॉक्सी अनुबंध के साथ इंटरैक्ट करते हैं, जो डेटा संग्रहीत करता है, लेकिन व्यावसायिक तर्क नहीं रखता है।

2. प्रॉक्सी अनुबंध तर्क अनुबंध के पते को संग्रहीत करता है और `delegatecall` फ़ंक्शन का उपयोग करके सभी फ़ंक्शन कॉल को तर्क अनुबंध (जो व्यावसायिक तर्क रखता है) को प्रत्यायोजित करता है।

3. कॉल को तर्क अनुबंध को अग्रेषित करने के बाद, तर्क अनुबंध से लौटाया गया डेटा पुनर्प्राप्त किया जाता है और उपयोगकर्ता को लौटा दिया जाता है।

प्रॉक्सी पैटर्न का उपयोग करने के लिए **delegatecall** फ़ंक्शन की समझ की आवश्यकता होती है। मूल रूप से, `delegatecall` एक ऑपकोड है जो अनुबंध को दूसरे अनुबंध को कॉल करने की अनुमति देता है, जबकि वास्तविक कोड निष्पादन कॉलिंग अनुबंध के संदर्भ में होता है। प्रॉक्सी पैटर्न में `delegatecall` का उपयोग करने का एक निहितार्थ यह है कि प्रॉक्सी अनुबंध अपने स्‍टोरेज को पढ़ता है और लिखता है और तर्क अनुबंध पर संग्रहीत तर्क को निष्पादित करता है जैसे कि आंतरिक फ़ंक्शन को कॉल करना।

[Solidity डॉक्यूमेंटेशन](https://docs.soliditylang.org/en/latest/introduction-to-smart-contracts.html#delegatecall-callcode-and-libraries) से:

> _**delegatecall** नामक संदेश कॉल का एक विशेष संस्करण मौजूद है जो इस तथ्य के अलावा एक संदेश कॉल के समान है कि लक्ष्य पते पर कोड कॉलिंग अनुबंध के संदर्भ (यानी पते पर) में निष्पादित किया जाता है और `msg.sender` और `msg.value` अपने मान नहीं बदलते हैं।_ _इसका मतलब है कि एक अनुबंध रनटाइम पर एक अलग पते से डायनेमिक रूप से कोड लोड कर सकता है। स्‍टोरेज, वर्तमान पता और शेष अभी भी कॉलिंग अनुबंध को संदर्भित करते हैं, केवल कोड को पते से लिया जाता है।_

जब भी कोई उपयोगकर्ता किसी फ़ंक्शन को कॉल करता है तो प्रॉक्सी अनुबंध `delegatecall` को इनवोक करना जानता है क्योंकि इसमें `fallback` फ़ंक्शन बनाया गया है। जब कोई फ़ंक्शन कॉल अनुबंध में निर्दिष्ट फ़ंक्शन से मेल नहीं खाता है तो Solidity प्रोग्रामिंग में [फ़ॉलबैक फ़ंक्शन](https://docs.soliditylang.org/en/latest/contracts.html#fallback-function) निष्पादित किया जाता है।

प्रॉक्सी पैटर्न को काम करने के लिए एक कस्टम फ़ॉलबैक फ़ंक्शन लिखने की आवश्यकता होती है जो निर्दिष्ट करता है कि प्रॉक्सी अनुबंध को फ़ंक्शन कॉल को कैसे प्रबंधित करना चाहिए, यह समर्थन नहीं करता है। इस मामले में प्रॉक्सी के फ़ॉलबैक फ़ंक्शन को एक delegatecall शुरू करने और वर्तमान तर्क अनुबंध कार्यान्वयन के लिए उपयोगकर्ता के अनुरोध को फिर से रूट करने के लिए प्रोग्राम किया गया है।

प्रॉक्सी अनुबंध डिफ़ॉल्ट रूप से अपरिवर्तनीय है, लेकिन अद्यतन किए गए व्यावसायिक तर्क के साथ नए तर्क अनुबंध बनाए जा सकते हैं। अपग्रेड करना तब प्रॉक्सी अनुबंध में संदर्भित तर्क अनुबंध के पते को बदलने का मामला है।

प्रॉक्सी अनुबंध को एक नए तर्क अनुबंध पर इंगित करके, कोड निष्पादित होता है जब उपयोगकर्ता प्रॉक्सी अनुबंध फ़ंक्शन से जुड़े बदलावों को कॉल करते हैं। यह हमें उपयोगकर्ताओं को एक नए अनुबंध के साथ बातचीत करने के लिए कहे बिना अनुबंध के तर्क को अपग्रेड करने की अनुमति देता है।

प्रॉक्सी पैटर्न स्मार्ट अनुबंधों को अपग्रेड करने के लिए एक लोकप्रिय तरीका है, क्योंकि वे अनुबंध माइग्रेशन से जुड़ी कठिनाइयों को समाप्त करते हैं। हालांकि, प्रॉक्सी पैटर्न उपयोग करने के लिए अधिक जटिल हैं और अनुचित तरीके से उपयोग किए जाने पर [फ़ंक्शन चयनकर्ता संघर्ष](https://medium.com/nomic-foundation-blog/malicious-backdoors-in-ethereum-proxies-62629adf3357) जैसे महत्वपूर्ण दोषों को पेश कर सकते हैं।

[प्रॉक्सी पैटर्न पर अधिक](https://blog.openzeppelin.com/proxy-patterns/)।

### अपग्रेड मैकेनिज़्म #4: स्ट्रैटेजी पैटर्न {#strategy-pattern}

यह तकनीक [रणनीति पैटर्न](https://en.wikipedia.org/wiki/Strategy_pattern) से प्रभावित है, जो विशिष्ट विशेषताओं को लागू करने के लिए अन्य प्रोग्राम के साथ इंटरफेस करने वाले सॉफ्टवेयर प्रोग्राम बनाने को प्रोत्साहित करती है। एथेरियम विकास के लिए स्ट्रैटेजी पैटर्न को लागू करने का मतलब एक स्मार्ट अनुबंध बनाना होगा जो अन्य अनुबंधों से कार्यों को कॉल करता है।

इस मामले में मुख्य अनुबंध में मुख्य व्यवसाय तर्क शामिल है, लेकिन कुछ कार्यों को निष्पादित करने के लिए अन्य स्मार्ट अनुबंधों ("उपग्रह अनुबंध") के साथ इंटरफ़ेस करता है। यह मुख्य अनुबंध हर उपग्रह अनुबंध के लिए पता भी संग्रहीत करता है और हर अनुबंध के अलग-अलग कार्यान्वयन के बीच स्विच कर सकता है।

आप एक नया उपग्रह अनुबंध बना सकते हैं और नए पते के साथ मुख्य अनुबंध को कॉन्फ़िगर कर सकते हैं। यह आपको स्मार्ट अनुबंध के लिए _रणनीतियों_ (यानी, नए तर्क को लागू करने) को बदलने की अनुमति देता है।

हालांकि पहले चर्चा किए गए प्रॉक्सी पैटर्न के समान, स्ट्रैटेजी पैटर्न अलग है क्योंकि मुख्य अनुबंध, जिसके साथ उपयोगकर्ता बातचीत करते हैं, व्यावसायिक तर्क रखता है। इस पैटर्न का उपयोग करने से आपको मुख्य बुनियादी ढांचे को प्रभावित किए बिना एक स्मार्ट अनुबंध में सीमित बदलाव पेश करने का अवसर मिलता है।

मुख्य समस्या यह है कि यह पैटर्न ज़्यादातर मामूली अपग्रेड को रोल आउट करने के लिए उपयोगी है। साथ ही, यदि मुख्य अनुबंध से समझौता किया जाता है (उदाहरण के लिए, हैक के माध्यम से), तो आप इस अपग्रेड विधि का उपयोग नहीं कर सकते।

### अपग्रेड मैकेनिज़्म #5: डायमंड पैटर्न {#diamond-pattern}

डायमंड पैटर्न को प्रॉक्सी पैटर्न पर सुधार माना जा सकता है। डायमंड पैटर्न प्रॉक्सी पैटर्न से भिन्न होते हैं क्योंकि डायमंड प्रॉक्सी अनुबंध फ़ंक्शन कॉल को एक से अधिक तर्क अनुबंध में सौंप सकता है।

हीरे के पैटर्न में तर्क अनुबंधों को _पहलुओं_ के रूप में जाना जाता है। डायमंड पैटर्न को काम करने के लिए, आपको प्रॉक्सी कॉन्ट्रैक्ट में एक मैपिंग बनाने की आवश्यकता है जो [फ़ंक्शन चयनकर्ताओं](https://docs.soliditylang.org/en/latest/abi-spec.html#function-selector) को अलग-अलग पहलू पतों पर मैप करता है।

जब कोई उपयोगकर्ता फ़ंक्शन कॉल करता है, तो प्रॉक्सी अनुबंध उस फ़ंक्शन को निष्पादित करने के लिए ज़िम्मेदार पहलू को खोजने के लिए मैपिंग की जांच करता है। फिर यह `delegatecall` (फ़ॉलबैक फ़ंक्शन का उपयोग करके) को आमंत्रित करता है और कॉल को उपयुक्त तर्क अनुबंध पर पुनर्निर्देशित करता है।

डायमंड अपग्रेड पैटर्न के मुकाबले पारंपरिक प्रॉक्सी अपग्रेड पैटर्न के कुछ फ़ायदे हैं:

1. यह आपको सभी कोड को बदले बिना अनुबंध के एक छोटे से हिस्से को अपग्रेड करने की अनुमति देता है। अपग्रेड के लिए प्रॉक्सी पैटर्न का उपयोग करने के लिए एक पूरी तरह से नया तर्क अनुबंध बनाने की आवश्यकता होती है, यहां तक कि मामूली अपग्रेड के लिए भी है।

2. सभी स्मार्ट अनुबंधों (प्रॉक्सी पैटर्न में उपयोग किए जाने वाले तर्क अनुबंधों सहित) में 24KB आकार सीमा होती है, जो एक सीमा हो सकती है - विशेष रूप से जटिल अनुबंधों के लिए अधिक कार्यों की आवश्यकता होती है। डायमंड पैटर्न कई तर्क अनुबंधों में कार्यों को विभाजित करके इस समस्या को हल करना आसान बनाता है।

3. प्रॉक्सी पैटर्न एक्सेस कंट्रोल के लिए कैच-ऑल दृष्टिकोण अपनाते हैं। अपग्रेड फ़ंक्शंस तक पहुँच रखने वाला निकाय _संपूर्ण_ अनुबंध को बदल सकता है। लेकिन डायमंड पैटर्न एक मॉड्यूलर अनुमति दृष्टिकोण को सक्षम बनाता है, जहां आप स्मार्ट अनुबंध के भीतर कुछ कार्यों को अपग्रेड करने के लिए संस्थाओं को प्रतिबंधित कर सकते हैं।

[हीरे के पैटर्न पर अधिक](https://eip2535diamonds.substack.com/p/introduction-to-the-diamond-standard?s=w)।

## स्मार्ट अनुबंधों को अपग्रेड करने के लाभ और हानि {#pros-and-cons-of-upgrading-smart-contracts}

| पेशेवरों                                                                                                                                | विपक्ष                                                                                                                                                           |
| --------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| एक स्मार्ट अनुबंध अपग्रेड परिनियोजन के बाद के चरण में खोजी गई कमजोरियों को ठीक करना आसान बना सकता है।                                   | स्मार्ट अनुबंधों को अपग्रेड करना कोड अपरिवर्तनीयता के विचार को नकारता है, जिसमें विकेंद्रीकरण और सुरक्षा के लिए निहितार्थ हैं।                                   |
| विकेन्द्रीकृत अनुप्रयोगों में नई सुविधाओं को जोड़ने के लिए डेवलपर्स तर्क को अपग्रेड करने की प्रोसेस का उपयोग कर सकते हैं।               | उपयोगकर्ताओं को डेवलपर्स पर भरोसा करना चाहिए कि वे स्मार्ट अनुबंधों में मनमाने ढंग से बदलाव न करें।                                                              |
| स्मार्ट अनुबंध अपग्रेड करने से अंतिम उपयोगकर्ताओं के लिए सुरक्षा में सुधार किया जा सकता है, क्योंकि बग को जल्दी से ठीक किया जा सकता है। | प्रोग्रामिंग स्मार्ट अनुबंधों में कार्यक्षमता को अपग्रेड करता है जटिलता की एक और परत जोड़ता है और महत्वपूर्ण खामियों की संभावना को बढ़ाता है।                    |
| अनुबंध उन्नयन डेवलपर्स को अलग-अलग सुविधाओं के साथ प्रयोग करने और समय के साथ डैप्स को बेहतर बनाने के लिए अधिक जगह देता है।               | स्मार्ट अनुबंधों को अपग्रेड करने का अवसर डेवलपर्स को विकास के चरण के दौरान उचित परिश्रम किए बिना परियोजनाओं को तेजी से लॉन्च करने के लिए प्रोत्साहित कर सकता है। |
|                                                                                                                                         | स्मार्ट अनुबंधों में असुरक्षित अभिगम नियंत्रण या केंद्रीकरण दुर्भावनापूर्ण अभिनेताओं के लिए अनधिकृत रूप से अपग्रेड करना आसान बना सकता है।                        |

## स्मार्ट अनुबंधों को अपग्रेड करने के लिए विचार {#considerations-for-upgrading-smart-contracts}

1. अनधिकृत स्मार्ट अनुबंध के अपग्रेड को रोकने के लिए सुरक्षित अभिगम नियंत्रण/प्राधिकरण तंत्र का उपयोग करें, खासकर यदि प्रॉक्सी पैटर्न, रणनीति पैटर्न या डेटा पृथक्करण का उपयोग कर रहे हैं। एक उदाहरण अपग्रेड फ़ंक्शन तक पहुंच को प्रतिबंधित कर रहा है, जैसे कि केवल अनुबंध का स्वामी ही इसे कॉल कर सकता है।

2. स्मार्ट अनुबंधों को अपग्रेड करना एक जटिल गतिविधि है और कमजोरियों की शुरुआत को रोकने के लिए उच्च स्तर के परिश्रम की आवश्यकता होती है।

3. अपग्रेड को लागू करने की प्रक्रिया को विकेन्द्रीकृत करके विश्वास मान्यताओं को कम करें। संभावित रणनीतियों में अपग्रेड को नियंत्रित करने के लिए [मल्टी-सिग वॉलेट कॉन्ट्रैक्ट](/developers/docs/smart-contracts/#multisig) का उपयोग करना, या अपग्रेड को अनुमोदित करने के लिए मतदान करने के लिए [डीएओ के सदस्यों](/dao/) की आवश्यकता होती है।

4. अनुबंधों को अपग्रेड करने में शामिल लागतों से अवगत रहें। उदाहरण के लिए, अनुबंध माइग्रेशन के दौरान एक पुराने अनुबंध से एक नए अनुबंध में राज्य (जैसे, उपयोगकर्ता शेष) की प्रतिलिपि बनाने के लिए एक से अधिक लेनदेन की आवश्यकता हो सकती है, जिसका अर्थ है अधिक गैस शुल्क।

5. उपयोगकर्ताओं की सुरक्षा के लिए **टाइमलॉक** लागू करने पर विचार करें। एक टाइमलॉक एक सिस्टम में परिवर्तन पर लागू देरी को संदर्भित करता है। अपग्रेड को नियंत्रित करने के लिए टाइमलॉक को मल्टी-सिग गवर्नेंस सिस्टम के साथ जोड़ा जा सकता है: अगर कोई प्रस्तावित कार्रवाई आवश्यक अनुमोदन सीमा तक पहुंच जाती है, तो यह पूर्वनिर्धारित विलंब अवधि समाप्त होने तक निष्पादित नहीं होती है।

टाइमलॉक उपयोगकर्ताओं को सिस्टम से बाहर निकलने के लिए कुछ समय देते हैं अगर वे प्रस्तावित परिवर्तन (जैसे, तर्क का अपग्रेड या नई शुल्क योजनाओं) से असहमत हैं। टाइमलॉक के बिना, उपयोगकर्ताओं को डेवलपर्स पर भरोसा करने की आवश्यकता है कि वे बिना किसी पूर्व सूचना के स्मार्ट अनुबंध में मनमाने ढंग से बदलाव लागू न करें। यहां दोष यह है कि टाइमलॉक कमजोरियों को जल्दी से पैच करने की क्षमता को प्रतिबंधित करता है।

## संसाधन {#resources}

**OpenZeppelin अपग्रेड प्लगइन्स - _अपग्रेड करने योग्य स्मार्ट अनुबंधों को लागू करने और सुरक्षित करने के लिए टूल्‍स का एक सूट।_**

- [GitHub](https://github.com/OpenZeppelin/openzeppelin-upgrades)
- [प्रलेखन](https://docs.openzeppelin.com/upgrades)

## ट्यूटोरियल {#tutorials}

- पैट्रिक कॉलिन्स के अनुसार [अपने स्मार्ट अनुबंधों को अपग्रेड करना | YouTube ट्यूटोरियल](https://www.youtube.com/watch?v=bdXJmWajZRY)
- ऑस्टिन ग्रिफ़िथ के अनुसार [एथेरियम स्मार्ट अनुबंध माइग्रेशन ट्यूटोरियल](https://medium.com/coinmonks/ethereum-smart-contract-migration-13f6f12539bd)
- प्रणेश ए.एस. के अनुसार, [स्मार्ट अनुबंधों को अपग्रेड करने के लिए UUPS प्रॉक्सी पैटर्न का उपयोग करना](https://blog.logrocket.com/author/praneshas/)
- Web3 ट्यूटोरियल: fangjun.eth के अनुसार [OpenZeppelin का उपयोग करके अपग्रेड करने योग्य स्मार्ट अनुबंध (प्रॉक्सी) लिखें](https://dev.to/yakult/tutorial-write-upgradeable-smart-contract-proxy-contract-with-openzeppelin-1916)

## अग्रिम पठन {#further-reading}

- सैंटियागो पल्लाडिनो के अनुसार [स्मार्ट अनुबंध उन्नयन की स्थिति](https://blog.openzeppelin.com/the-state-of-smart-contract-upgrades/)
- [Solidity स्मार्ट अनुबंध को अपग्रेड करने के कई तरीके](https://cryptomarketpool.com/multiple-ways-to-upgrade-a-solidity-smart-contract/) - क्रिप्टो मार्केट पूल ब्लॉग
- [जानें: स्मार्ट अनुबंध को अपग्रेड करना](https://docs.openzeppelin.com/learn/upgrading-smart-contracts) - OpenZeppelin डॉक्स
- नवीन साहू के अनुसार, [Solidity कॉन्ट्रैक्ट्स की अपग्रेडेबिलिटी के लिए प्रॉक्सी पैटर्न: ट्रांसपेरेंट बनाम UUPS प्रॉक्सी](https://mirror.xyz/0xB38709B8198d147cc9Ff9C133838a044d78B064B/M7oTptQkBGXxox-tk9VJjL66E1V8BUF0GF79MMK4YG0)
- निक मडगे के अनुसार, [डायमंड अपग्रेड कैसे काम करता है](https://dev.to/mudgen/how-diamond-upgrades-work-417j)