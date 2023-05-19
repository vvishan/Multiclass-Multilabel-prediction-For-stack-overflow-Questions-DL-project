"# Stackoverflow" 
In the given project we gonna find the Titles and bodys that are assosiated with the tags.

step1: We are taking the Tags csv file by using the collections library we are able find the 10 most common tags with in the csv and plot them.
step2: And then we assigning new variable for top 10 tags , and then writig the defination to sagrigate the ids on tags, by using the apply method 
step3: Then we have dropped the duplicate.and we have made the tags.csv file ready.
step4: Now taking the question csv for data cleaning.
step5: Now removing the unwanted columns from the csv using the drop and considering only ID,Title and Body columns.
step6: Now we need to clean the data in that columns as the columns contains the text, so we used the regex funtion and def a function to remove the unwanted symbols then we have used the apply method using that function on it.
step7: After cleaning the data we have merged the both the Tags.csv and question.csv on IDs

step8:Using the MultiLabelBinarizer from sklearn.preprocessing we are able to fit on the total tags and create the label classes.
step9:Now usint the train_test_split from sklearn model_selection we have divided the data into tarin and test.
step10:Now we have assigined the variable for each text columns in train and test data. and for each coulmn we have taken the sentence length using the len(word_tokenize()) and then we are taking the quantile length of each column.
step11:Then we use the Tokenizer(char_level=False,split=' '),fit_on_texts,texts_to_sequence on the each columns and calculating the vocab size of each column using the len(index_word.keys()) and arraged the pad_sequeence using the texts_to_sequence and word_tokenize  quantile length.

step12 : Now to coming to the model we are creating the RNN model to predict the tags associated with the questions, so we need to take the both bady and title columns seperate inputs to embed with the shape of  max_len on each columns word_tokenize.
step13: After embed the both the columns text input columns with shape of max-len from word_tokenize then we need to concat them and we have added the dense layers , dropouts and Batchnormalization we atking the output dims as 10 with activation function functon as sigmoid and initiating the model as model=Model(inputs=[title_input,body_input],outputs=[main_output,auxiliary_output]).

step13: Now we compile the model with loss and optimizer as 
model.compile(loss={'main_output':'categorical_crossentropy','auxiliary_output':'categorical_crossentropy'},optimizer='adam'
              ,metrics=['accuracy'])
              
step14: model fitting 
results=model.fit({'title_input':sequence_marix_train_t,'body_input': sequence_matrix_train_b},
                 {'main_output':y_train,'auxiliary_output':y_train},
                 validation_data=[{'title_input':sequence_matrix_test_t,'body_input':sequence_matrix_test_b},
                 {'main_output':y_test,'auxiliary_output':y_test}],
                 epochs=5,batch_size=800)
