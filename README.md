# COURSERAPROJ1_30224
CREATE TABLE public.product_type (
    type_id integer NOT NULL,
    category character varying(50),
    type character varying(50),
    CONSTRAINT product_type_pkey PRIMARY KEY (type_id)
);

CREATE TABLE public.product (
    product_id integer NOT NULL,
    type_id integer,
    name character varying(50),
    description character varying(255),
    price money,
    CONSTRAINT product_pkey PRIMARY KEY (product_id)
);

ALTER TABLE public.product
ADD CONSTRAINT product_type_fkey FOREIGN KEY (type_id)
REFERENCES public.product_type (type_id);

CREATE TABLE public.sales_transaction (
    transaction_id integer NOT NULL,
    date date,
    time time with time zone,
    sales_outlet_id integer,
    staff_id integer,
    customer_id integer,
    CONSTRAINT sales_transaction_pkey PRIMARY KEY (transaction_id)
);

CREATE TABLE public.sales_detail (
    sales_detail_id integer NOT NULL,
    transaction_id integer,
    product_id integer,
    quantity integer,
    price money,
    CONSTRAINT sales_detail_pkey PRIMARY KEY (sales_detail_id)
);

ALTER TABLE public.sales_detail
ADD CONSTRAINT sales_detail_product_fkey FOREIGN KEY (product_id)
REFERENCES public.product (product_id);

ALTER TABLE public.sales_detail
ADD CONSTRAINT sales_detail_transaction_fkey FOREIGN KEY (transaction_id)
REFERENCES public.sales_transaction (transaction_id);
