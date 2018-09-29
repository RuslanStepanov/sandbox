# CONFIGURATION FULL TEXT SEARCH ADDRESS POSTGRES


https://www.postgresql.org/docs/9.5/static/textsearch.html

Добавление словарей и конфигурации

CREATE TEXT SEARCH DICTIONARY russian (
    TEMPLATE = ispell,
    DictFile = russian,
    AffFile = russian,
    StopWords = russian
);

CREATE TEXT SEARCH DICTIONARY ru_address_synonym(
	TEMPLATE = synonym,
    SYNONYMS  = russian_address
);

CREATE TEXT SEARCH CONFIGURATION ru_address (COPY=russian);

CREATE TEXT SEARCH DICTIONARY ru_address_thesaurus (
    TEMPLATE = thesaurus,
    DictFile = russian_address,
    Dictionary = russian
);


ALTER TEXT SEARCH CONFIGURATION ru_address 
	ALTER MAPPING FOR hword, hword_part, word 
    WITH ru_address_synonym, ru_address_thesaurus, russian, russian_stem;


Удалить словари


drop text search configuration ru_address;
drop text search dictionary ru_address_thesaurus;
drop text search dictionary ru_address_synonym;
drop text search dictionary russian;
